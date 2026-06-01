# Statistical Inference (Prof. Hyungsuk Tak)

## Review

- A random variable is a mapping rule, assigning a number to each object in the Sample Space.
- The random variables we learn in probability are the features of my dataset.
- The statistical inferencing starts from the assumption that the elements of a dataset column are some number of random realizations from a distribution.
- While this assumption may be wrong, it helps us draw inference from the data.
- We can have multiple possibilities of parent distrbution for a given sample.

## Terminology

1. **Population:** The entire set of objects we are interested in.
2. **Sample:** A fraction of the population from which we actually collect data.
3. **Statistical modelling:** It's an effort to explain a potential data generation process, starting with an assumption that the data are r.v.s, and the observed data are random realizations of these data. Then we assume a specific probabilitiy distribution on the data to better understand the randomness (uncertainity) involved with the data.

- There are assumptions on the data:
    - The parameter of the distrbution might be coming from an actual Physical equation.
    - Bayesian prior on the parameters.

This set of assumptions are called a **Model**.

- In statistical modelling, the quantitiy of interest is expressed as the unknown parameter of a distribution.

- Two schools of thought:
    1. **Frequentist:** The unknown quantity of interest is a fixed constant.
    2. **Bayesian:** The uniknown quantity of interest is a random variable.

3. **Estimator:** A numerical summary (i.e., function) of the data, like mean, median, maximum, etc to infer the parameter $\theta$. This is an r.v., because a function of rvs should also be an r.v.It is written as $\hat{\theta}$.

- A specific value of the estimator from data is called an estimate.

## Probability and Statistical Inference

- Statistical inference is estimatign the model parameter, $\theta$, given the data.

## Mean-squared error

$$
{\rm MSE}(\hat{\theta}) = {\rm Bias}^2(\hat{\theta}) + {\rm Var}(\hat{\theta})
$$

- **Bias:** Refers to the how far away is an estimate (mean) from the actual parmeter value.
- **Variance:** Refers to the spread in the data

- A good estimator will have less bias and less variance.
- MSE balances out bias and variance, thus, is in use.
- Root MSE (RMSE) is also used frequently.

## Maximum Likelihood Estimation
#### Likelihood function
- Ot is defined as the joint probability density, or mass function, of the observed data $x={x_1, x_2, x_3,...,X_n}$ (fixed constants), viewd as a function of $\theta$.

$$
\ell(\theta)= f(x|\theta) = f(x_1, x_2,...,x_n|\theta)=\prod_{i=1}^n f(x_i|\theta)
$$

- Likelihood function speaks for the data about which parameter do the given set of data prefer.

#### MLE Estimator
- Finding the point in the parameter space which maximizes the likelihood of the parameters.
- Note that we use $\log\ell(\theta)$ because it's computationally less expensive to perform addition, than multiplication.
- MLE is unbiased, most efficient (smallest variance) and approximately Normally distrbuted estimator for large $n$.

$$
\hat{\theta}_{\rm MLE} \sim \mathcal{N}(\theta, \hat{\tau}_n^2)
$$

- The asymptotic uncertainity of the MLE $\hat{\theta}$, $\hat{\tau}_n^2$ can be numerically computed with the Hessian matrix.

$$
H = \nabla\nabla l(\theta) = \frac{\partial^2}{\partial\theta\partial\theta^*}l(\theta)
$$

- $(-H)^{-1}$ will have diagonal matrix elements as the uncertainity of the parameter estimates.

#### Limitations
- Sometimes biased when small sample size
- Doesn't always have a closed-form solution

## Confidence Interval
- The reported $1\sigma$ on astronomical parameter estimates is obtained from the Hessian matrix.

- For a given value of $\alpha\in(0,1)$ (typically, $\alpha=0.05$ in statistics and $\alpha=0.32$ in astronomy), an $100(1-\alpha)\%$ confidence interval for $\theta$ is defined as an interval $(l(X), u(X))$, such that,

$$
P(l(X)< \theta < u(X)) = 1-\alpha
$$

- Note that the upper and lower bounds are random variables too. Thus, we use "a $95\%$ confidence interval, and not "the $95\%$ confidence interval."

- If we were to draw a 1000 intervals, about $95\%$ of the intervals would contain the true value of $\theta$

## Hypothesis Testing

- **Estimation:** Pinning down the underlying values of unknown parameters from a potentially large number of possibilities with plausible range of parameter values.
- **Hypothesis testing:** Given two hypothesis about the parameter value, which one do the data support more?

### Terminology
1. **Statistical hypothesis:** A statement about parameters(s) $\theta$ of a pdf
2. **Null vs alternative:** The null hypothesis represents the default case, and the alternative represents what the researcher wants to argue.
3. **Test statistic:** Let $T=h(X_1, X_2, .., X_n)$ be a function of the data to be used to determine which hypothesis is supported more by the data. Then we call it a test statistic.
4. **Significance level:** The same $\alpha$ used in confidence interval. A test with significance level of $\alpha0.05$ means that the test controls the probability of rejecting H_0 when it is the case, i.e., P(reject $\theta_0$| $\theta_0$ is the case), to be smaller than or equal to 0.05.

### Principle in hypothesis testing
- We assume that the null hypothesis is true.
- Find the distribution of the test statistic under $\theta_0$.
- Check whether the evidence in the data in within the probability range of this distribution.
- If $T$ is realized far from the null distribution, it is a strong evidence against the null hypothesis.
- If null hypothesis were true, $T$ would be realised near the density region of the distribution.

### Likelihood ratio test
- Let $H_0:\theta=\theta_0$ and $H_1: \theta=\theta_1$
- We compare likelihoods $\ell(\theta_0)$ and $\ell(\theta_1)$, and check which one would the data prefer.
- **Neyman-Pearson Lemma:** The likelihood test maximizies the probabilitiy of rejecting $H_0$ when $H_0$ is not the case.

## Model Comparison
### Limitations of likelihood ratio test
1. Only applicable to nested models (i.e., the model under $H_0$ is a special case of the model under $H_1$)
2. Likelihood functions always prefer more complex models.

- We use 'penalized likelihood test' for model comparison.

### Akaike information criterion

$$
{\rm AIC}=-2\ell(\hat{\theta})+2p
$$ 

- where $\ell(\hat{theta})$ is the maximized log-likelihood and $p$ is the number of parameters in the model.
- A model with smallest AIC will be the simplest and the best explanation of the data.

### Bayesian information criterion

$$
{\rm BIC}=-2\ell(\hat{\theta}) + \ln(n)p
$$

- As we collect more data, the penalty on an additional parameter becomes stronger than AIC
