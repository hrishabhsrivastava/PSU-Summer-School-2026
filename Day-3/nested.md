# Nested Sampling (Dr. Joshua Speagle, UToronto)

## Past

The discussion about the need of Nested Sampling and how did we get here

### Background

- It starts from Bayes theorem: Posterior = (likelihood x Prior)/Evidence

### Motivation

- Sampling the posterior
- Solving an MCMC is a hard problem, done once
- Nested Sampling solves an easier problem multiple times
    - Instead of sampling from a complex distribution once, nested sampling samples from a 'uniform distribution' in a multiple nested steps
    - The goal is to generate a sample in an iteration, assign a 'volume' to it, generate a sample inside the volumne, then assign a new volume inside and repeat the steps
    - We keep on sampling uniformly. There's way to move it from uniform distribution to a different distribution.

- MCMC is a 'frequentist' approach to a Byesian problem
- Nested Sampling guarantees finite-sample, unlike MCMC which can keep on running but mightn'y converge't

#### Integrating the prior
- The idea is to construct a 'prior volume' shells

$$
X(\lambda) \equiv \int_{\Theta:\ell(\Theta)>\lambda} \pi(\Theta) d\Theta
$$ 

- Then take these slices and sample likelihood 'uniformly' from them

$$
Z = \int_0^1 \ell(L)(X)dX \sim \sum_{i=1}^n \ell_i \times \Delta X_i
$$

- Lebesque Integral: As opposed to Riemannian integral, we are drawing slices in integration horizontally inside the function.
- Nested sampling gives you an estimator of $\Delta\hat{X}_i$

### Estimating prior volume
- The idea is to generate samples such that my likelihood at every iteration just needs to be greater than the likelihood of the previous iteration
- I generate the likelihood by sampling uniformly from the prior 

---

### Corrected Nested Sampling Algorithm

1. **Initialize:** Draw a set of $N$ "live points" from the prior distribution $\pi(\theta)$.
2. **Identify:** Find the live point with the lowest likelihood, $L_i$.
3. **Volume Update:** Estimate the new, smaller prior volume $X_i$ enclosed by the likelihood contour $L > L_i$.
4. **Replace (The Correction):** Discard this lowest-likelihood point. Draw exactly **one** new point from the prior, subject to the hard constraint that its likelihood is greater than $L_i$.
5. **Evidence Accumulation:** Calculate the volume weight $\Delta X_i$ and add the differential evidence $\Delta Z_i = L_i \Delta X_i$ to the total evidence $Z$.
6. **Terminate:** Repeat steps 2–5 until the estimated remaining evidence is smaller than a defined tolerance threshold.

---

### The Mathematical Framework

Nested sampling maps a multi-dimensional parameter space onto a one-dimensional variable, making it incredibly powerful for exploring highly non-linear or multi-modal posteriors—such as those encountered when classifying and modeling strong gravitational lenses. 

Here is the math driving the engine at each step.

#### 1. The Prior Volume ($X$)
Nested sampling defines $X(\lambda)$ as the fraction of the prior volume where the likelihood $L(\theta)$ is greater than $\lambda$:

$$
X(\lambda) = \int_{L(\theta) > \lambda} \pi(\theta) d\theta
$$

The volume starts at $X_0 = 1$ (the entire parameter space) and systematically shrinks toward $X = 0$ (the maximum likelihood peak).

#### 2. The Evidence ($Z$)
The primary goal of nested sampling is calculating the Bayesian Evidence ($Z$). The total evidence is the integral of the likelihood over the prior volume:

$$
Z = \int_{0}^{1} L(X) dX
$$
We approximate this integral numerically as a sum over our iterations $i$:

$$
Z \approx \sum_{i=1}^{M} L_i \Delta X_i
$$

#### 3. Volume Shrinking (Statistical vs. Exponential)
At each step $i$, the volume shrinks. Because the $N$ live points are uniformly distributed within the current prior volume $X_{i-1}$, the shrinkage factor $t_i = X_i / X_{i-1}$ follows the distribution of the largest of $N$ uniform random variables from $[0, 1]$. 

* **Statistical Shrinking:** You can simulate the exact statistical uncertainty by drawing $t_i$ from a Beta distribution at each step: $t_i \sim \text{Beta}(N, 1)$, giving $X_i = t_i X_{i-1}$.
* **Exponential (Deterministic) Shrinking:** For large $N$, the statistical fluctuations average out. The expected value of $\ln(t)$ is $E[\ln(t)] = -1/N$. Therefore, we can deterministically approximate the volume at step $i$ using exponential decay:

$$
X_i \approx \exp\left(-\frac{i}{N}\right)
$$

#### 4. Calculating $\Delta X_i$ (Linear vs. Trapezoidal)
To calculate the weight of the $i$-th shell, we need the width $\Delta X_i$.
* **Linear/Simple Difference:**

$$
\Delta X_i = X_{i-1} - X_i
$$

* **Trapezoidal Rule:** This is generally preferred as it provides a more accurate numerical integration over the curve:

$$
\Delta X_i = \frac{1}{2}(X_{i-1} - X_{i+1})
$$

#### 5. Posterior Weights ($w_i$)
While MCMC walks the parameter space to yield posterior samples directly, nested sampling provides them as a byproduct. Each discarded point $i$ represents a shell of parameter space. Its statistical weight is simply the fraction of the total evidence it contributed:

$$
w_i = \frac{L_i \Delta X_i}{Z}
$$

To generate a chain of equal-weight posterior samples, you take the full set of discarded points and resample them according to these weights $w_i$.

#### 6. Stopping Criterion
The algorithm terminates when the remaining volume cannot substantially change the total evidence. The maximum possible remaining evidence ($\Delta Z_{\text{remaining}}$) is bounded by assuming the remaining prior volume ($X_M$) all possesses the maximum likelihood found so far ($L_{\text{max}}$):

$$
\Delta Z_{\text{remaining}} \approx L_{\text{max}} X_M
$$

When $\frac{\Delta Z_{\text{remaining}}}{Z} < \text{tolerance}$, the run is complete. 

