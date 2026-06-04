# Markov Chain Monte Carlo (Dr. Murali Haran, PSU)

## Monte Carlo
- It is an appraoch for approximating integrals
- Our goal is to approximate expectations
- We draw many samples from a distribution and approximate samples.

**Simple Monte Carlo**
- Samples are IID
- Determined quality of approximation $\hat{\mu}_m$ by:

$$
\text{std deviation}(\hat{\mu}_m)/\sqrt{m}
$$

- This standard deviation is small enough if $m$ is large enough!

## Markov Chain Monte Carlo

- Unlike basic MC, $\hat{\mu}_m$ is biased and based on samples which are neither independent, nor identically distributed.
- Need to work a little harder to ensure the quality of the estimation.
- MCMC gives a general recipe for constructing markov chains for Bayesian posterior
- Use the Metropolis-Hastings Algorithm

**MCMC Diagnostic**
- Variability: MCMC std dev is done via batch means or other tools, specific to MCMC. We cannot use s.dev/sqrt(m)
- Check for the starting value of related bias.
