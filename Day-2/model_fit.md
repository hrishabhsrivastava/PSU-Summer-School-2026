# Model Fitting

- Model fitting refers to the fitting of models based on observed data.
- It might involve a simple heuristic model to explain the data, or a complex model based on our understanding of the Physics.

## Qualities of a good model
- Parsimonious (simple)
- Conform goodness-of-fit
- Easily generalizable
- Neither underfit, nor overfit
- Low bias and variance

### Parameter estimation by $\chi^2$
- It is also known as 'weighted-least-squares'.
- It some some limitations:
    - Fails when there are too few points
    - Binning is arbitrary and leads to loss of information.
    - Assumes independence of data points
    - Doesn't differentiate


## Deep Dive into the Kolmogorov-Smirnov (KS) Test

The Kolmogorov-Smirnov (KS) test is an elegant, non-parametric statistical method used to determine if a sample matches a theoretical distribution, or if two independent samples share the same underlying distribution. Geometrically and visually, it is one of the most intuitive statistical tests because it fundamentally reduces down to measuring a single, maximum vertical distance on a 2D plot.

---

### 1. The Foundational Building Block: The Empirical Cumulative Distribution Function (EDF)

Before defining the Empirical CDF, let us recall the standard theoretical **Cumulative Distribution Function (CDF)**, typically denoted as $F(x)$. For a random variable $X$, the CDF evaluates the probability that $X$ takes a value less than or equal to a specific value $x$:

$$F(x) = P(X \le x)$$

An **Empirical CDF (EDF)**, denoted as $F_n(x)$, applies this exact same concept directly to a discrete, real-world dataset containing $n$ independent observations. 

#### Geometric Interpretation
Imagine sorting your data points in ascending order: $X_{(1)} \le X_{(2)} \le \dots \le X_{(n)}$. The EDF is a step function (or staircase) that begins at a y-value of $0$ at $-\infty$ and ends at a y-value of $1$ at $+\infty$. Every time you move past an observed data point along the x-axis, the staircase steps up by exactly $\frac{1}{n}$.

#### Mathematical Formulation
Mathematically, the EDF is expressed using an indicator function $\mathbb{I}$:

$$F_n(x) = \frac{1}{n} \sum_{i=1}^n \mathbb{I}_{(-\infty, x]}(X_i)$$

Where:
* $\mathbb{I}_{(-\infty, x]}(X_i) = 1$ if $X_i \le x$
* $\mathbb{I}_{(-\infty, x]}(X_i) = 0$ if $X_i > x$

---

### 2. The Heart of the Test: The KS Statistic ($D$)

The goal of the KS test is to quantify how much an empirical distribution deviates from a reference distribution. The metric used to capture this deviation is the **KS Statistic**, denoted as $D$.

The $D$ statistic is defined as the **supremum (absolute maximum) vertical distance** between the two curves being compared.

$$D = \sup_x |F_n(x) - F_0(x)|$$

#### Visualizing $D$
If you overlay the staircase plot of your empirical dataset ($F_n(x)$) with a smooth theoretical CDF curve ($F_0(x)$) on the same coordinate axes, $D$ represents the absolute longest vertical line segment you can draw to bridge the gap between the two functions.

* **$D \to 0$:** The empirical staircase tightly hugs the reference curve, signaling a high probability that the sample conforms to the reference distribution.
* **$D \to 1$:** A massive vertical divergence exists between the curves, signaling that the sample is highly unlikely to have originated from the reference distribution.

---

### 3. The Two Flavors of the KS Test

Depending on your scientific objective, the KS test is deployed in one of two configurations:

#### A. One-Sample KS Test
* **Objective:** Evaluates whether an empirical dataset sample follows a specified continuous theoretical distribution ($F_0(x)$), such as a standard Gaussian, Uniform, or Power-law distribution.
* **Example Application:** Testing whether the residual noise in an instrument's calibration data is truly Gaussian.

#### B. Two-Sample KS Test
* **Objective:** Compares two distinct, independent empirical datasets (Sample 1 with size $n$ and Sample 2 with size $m$) to determine if they are drawn from the same continuous, unspecified distribution.
* **Formulation:** $$D = \sup_x |F_n(x) - F_m(x)|$$
* **Example Application:** Determining whether the spatial clustering of two different populations of astronomical objects originates from identical underlying environmental fields.

---

### 4. Hypothesis Testing Framework

The decision-making architecture of the KS test adheres to standard frequentist null-hypothesis significance testing (NHST):

* **$H_0$ (Null Hypothesis):** The sample is drawn from the specified continuous distribution (One-Sample), or both samples are drawn from the identical underlying distribution (Two-Sample).
* **$H_1$ (Alternative Hypothesis):** The empirical distribution does not conform to the reference distribution.

#### The $p$-value Extraction
Once the maximum vertical distance $D$ is observed, it is compared against the limiting distribution of the Kolmogorov-Smirnov statistic (the Kolmogorov distribution). As sample size increases, the critical values scale inversely with $\sqrt{n}$.

* **High $p$-value ($p \ge \alpha$):** The observed vertical gap $D$ is small enough to be easily attributed to expected stochastic sampling noise. We **fail to reject** $H_0$.
* **Low $p$-value ($p < \alpha$):** The observed vertical gap $D$ is extreme, falling far into the tail of the null probability distribution. We **reject** $H_0$ and conclude a statistically significant difference exists.

---

### 5. Mathematical Strengths and Constraints

While powerful, the KS test exhibits specific behaviors that dictate when it should—and should not—be deployed.

#### Advantages
1. **Completely Non-Parametric:** It makes zero prior assumptions regarding the analytical form of the underlying distributions being evaluated.
2. **Eliminates Binning Artifacts:** Unlike the Pearson Chi-Squared ($\chi^2$) goodness-of-fit test, the KS test does not require grouping continuous data into arbitrary bins. Binning discards valuable localized structural information; the KS test operates natively on unbinned data points, maximizing statistical power.

#### Limitations & Sensitivities
1. **Central Domain Over-Sensitivity:** Because all CDFs are mathematically constrained to anchor at $(x=-\infty, y=0)$ and $(x=+\infty, y=1)$, the two curves naturally converge at both tails. Consequently, the test is highly sensitive to variations near the **median (center)** of the distribution, but remains relatively blind to variations in the **tails**. 
2. **Continuous Variable Strictness:** The underlying distribution must be continuous. If the data contains discrete ties (identical repeated values due to rounding or digitizing), the step heights are artificially inflated, causing the test to become overly conservative and skewing the resulting $p$-values.
3. **Parameter Estimation Vulnerability:** In its classic form, the one-sample KS test requires that the parameters of the theoretical distribution (e.g., the mean $\mu$ and variance $\sigma^2$ of a Gaussian) be known *a priori*. If you estimate these parameters directly from your sample before running the test, the standard KS $p$-values become invalid (in such cases, a modified test like the **Lilliefors test** or Monte Carlo calibrations must be used instead).


# Bootstrapping

Bootstrapping is a remarkably elegant and powerful non-parametric resampling technique. It is used to estimate the sampling distribution of a statistic directly from your data, bypassing the need for rigid theoretical assumptions about the underlying population.

---

## PART 1: The Core Philosophy and Basics

### 1. The Plug-In Principle
In traditional frequentist statistics, finding the standard error of a statistic requires drawing thousands of samples from the **true population**. In reality, you only have one dataset of size $n$. 

Bootstrapping operates on the assumption that **your sample is the best possible approximation of the entire population**. Because we don't know the true population distribution ($F$), we "plug in" our **Empirical Distribution** ($\hat{F}$), defined entirely by our observed data. 

* **Traditional:** Population $\to$ Samples $\to$ Statistic
* **Bootstrap:** Sample $\to$ Resamples $\to$ Bootstrap Statistic

### 2. The Mechanics: Sampling with Replacement
The engine driving bootstrapping is **sampling with replacement**. 
For a dataset $X = \{x_1, x_2, \dots, x_n\}$, a single bootstrap sample ($X^*$) is generated by randomly drawing $n$ data points from $X$, putting each point back into the pool before drawing the next. 

Because we replace the data, some original points will appear multiple times, while roughly $36.8\%$ will be omitted (Out-of-Bag data). This introduces the stochastic variation necessary to simulate drawing a new sample from the true population.

### 3. The Bootstrap Procedure
To build a bootstrap distribution for any statistic $\theta$ (mean, variance, correlation, etc.):
1. Calculate the observed statistic $\hat{\theta}$ from the original dataset.
2. Draw a bootstrap sample $X^*$ of size $n$ *with replacement*.
3. Compute the bootstrap statistic $\hat{\theta}^*$ on $X^*$.
4. Repeat Steps 2 and 3 a large number of times ($B$ times, e.g., $10,000$).

You are left with a collection of bootstrap estimates: $\{\hat{\theta}^*_1, \hat{\theta}^*_2, \dots, \hat{\theta}^*_B\}$.

### 4. Extracting Value from the Bootstrap Distribution
Once you plot the histogram of your $B$ estimates (the **Bootstrap Distribution**), you can extract metrics directly:

* **Bootstrap Standard Error:** The empirical standard deviation of your $B$ estimates:
  
    $$SE_{\text{boot}} = \sqrt{\frac{1}{B-1} \sum_{b=1}^B \left( \hat{\theta}^*_b - \bar{\theta}^* \right)^2}$$

* **Estimating Bias:** $\text{Bias}_{\text{boot}} = \bar{\theta}^* - \hat{\theta}$
* **Confidence Intervals (Percentile Method):** Sort the $B$ estimates. For a $95\%$ CI, the boundaries are the $2.5^{\text{th}}$ and $97.5^{\text{th}}$ percentiles of your sorted list.

---

## PART 2: The Mathematical Framework & Advanced Concepts

### 1. Formalizing the Distributions
* **The Reality:** Your dataset $X = (X_1, \dots, X_n)$ is drawn from true distribution $F$. Your estimator is $\hat{\theta} = h_n(X_1, \dots, X_n)$.
* **The Bootstrap Universe:** Your resample $X^* = (X^*_1, \dots, X^*_n)$ yields $\theta^* = h_n(X^*_1, \dots, X^*_n)$.

**The Golden Rule:** The variation of $(\theta^* - \hat{\theta})$ behaves almost exactly like the variation of $(\hat{\theta} - \theta)$.

### 2. Standardization / Studentization
Standardizing statistics makes them "units free" and forces the bootstrap distribution to converge to the true distribution much faster.

* **True Sampling Distribution ($G_n$):** $G_n(x) = P\left(\frac{\sqrt{n}(\bar{X} - \mu)}{\sigma} \le x\right)$
* **Bootstrap Distribution ($G_B$):** Applying the plug-in principle, we substitute our sample values for the unknown true parameters:
  
    $$G_B(x) = P^*\left(\frac{\sqrt{n}(\bar{X}^* - \bar{X})}{s_n} \le x \Big| X\right)$$
  
    *(where $s_n$ is the sample standard deviation).*
Because $G_n \approx G_B$, we use the computable $G_B$ as a perfect stand-in for the unknowable $G_n$.

### 3. Computational Reality and Confidence Intervals
Calculating all $M = n^n$ possible bootstrap combinations is impossible. Instead, we use $N$ random replications (where $N \ll M$, usually $N \sim n(\log n)^2$ or simply $10,000$). 

By calculating the studentized statistic $r_{ij} = \frac{\sqrt{n}(\bar{X}^{*(ij)} - \bar{X})}{s_n}$ for $N$ samples, sorting them ($v_1 < v_2 < \dots < v_N$), and extracting the lower ($v_k$) and upper ($v_m$) percentiles, we derive the robust CI:

$$\bar{X} - v_m \frac{s_n}{\sqrt{n}} \le \mu < \bar{X} - v_k \frac{s_n}{\sqrt{n}}$$

### 4. The Smooth Functional Model (Where Bootstrap Excels)
Bootstrapping works for any parameter $\theta$ that can be expressed as a **smooth function** $H$ of the data (i.e., continuous derivatives, no sharp jumps). This covers almost all common statistics:
* Sample Means & Variances
* Central and Non-central t-statistics
* Maximum Likelihood & Least Squares Estimators
* Correlation ($\rho$) & Regression Coefficients

### 5. Where the Bootstrap Fails
1. **Non-Smooth Estimators (e.g., Maximums):** If $\hat{\theta} = \max(X_i)$, the bootstrap sample can never exceed the original sample's maximum. The bootstrap distribution artificially clumps at the observed maximum, failing to model the true tail variation.
2. **Heavy Tails / Infinite Variance:** If $E[X_1^2] = \infty$, the Central Limit Theorem breaks down, and the sample mean wildly fluctuates based on extreme outliers.

### 6. Time-Series Data & The Moving Block Bootstrap
Standard bootstrapping assumes data is **I.I.D.** (Independent and Identically Distributed). For time-series or dependent data, sampling individual points with replacement destroys the temporal structure (autocorrelation).

**Solution - Moving Block Bootstrap:**
1. Split the time-series into overlapping blocks of length $b$ (e.g., Block 1 = Days 1 to $b$, Block 2 = Days 2 to $b+1$).
2. Draw these *entire blocks* at random with replacement.
3. Stitch them together to form a resampled timeline.
This preserves the local dependency structure within the blocks.

### 7. Nonparametric vs. Parametric Bootstrap
* **Nonparametric Bootstrap:** Sampling directly from the empirical data points (assuming nothing about the distribution shape).
* **Parametric Bootstrap:** Assuming the data follows a specific theoretical distribution (e.g., $N(\mu, \sigma^2)$). You estimate $\mu$ and $\sigma$ from your data, and then instruct a computer to generate entirely new, fake samples drawn from $N(\bar{X}, s^2_n)$.

### 8. Goodness-of-Fit and Fixing the KS Test
The classic Kolmogorov-Smirnov (KS) test requires the theoretical distribution parameters to be known *a priori*. If you estimate the parameters (like mean and variance) from your data and *then* run a KS test, your $p$-values will be artificially conservative and incorrect.

**The Parametric Bootstrap Fix:**
By using the parametric bootstrap to repeatedly simulate data from the estimated theoretical distribution, you can generate a custom, highly accurate distribution for the KS statistic ($D^*$). You then compare your observed KS statistic ($D$) against this bootstrapped distribution to get a valid $p$-value.

---

### Summary of Goodness-of-Fit Tests
* **EDF-based fitting** requires little to no distributional assumptions.
* **KS Test** is generally superior to the Chi-square test (as it avoids binning artifacts) but is blind to heteroscedastic errors and cannot easily handle multi-dimensional data.
* **Anderson-Darling Test** applies weighting to better handle discrepancies in the tails of the distribution.
* **Bootstrap** acts as the ultimate computational patch for complex scenarios, particularly when parameters are estimated from the data itself or when dealing with complex multi-dimensional statistics. 
