# Bayesian Inferencing (Dr. Tom Loredo, Cornell)

**Data:** Data are evidence in evidence-based reasoning.
**Statistical data analysis:** Quantifying uncertainities in inferences
**Inferencing:** Learning about the data generative process from the observed data

- The most fundamental principle of the statistical paradigm, its starting point, is that **variation** may be described by probability.
- The Bayesian approach states that the uncertainity may be described by probability.
- Probability quantifes uncertainity.

## Probability
- Classical probability is geberalized logic.
- Consider the following propositions: statements that may be true or false
    - P: Universe can be modelled with $\Lambda$CDM
    - A: $\Omega_{\rm tot}\in[0.9,1.1]$
    - B: $\Omega_\Lambda$ is not 0.
    - $\bar{B}$: $\Omega_\Lambda=0$

- Events in frequentist Probability theory are propositions about outcomes in repeated trials.

### Arguments
- Arguments: Assertion that a hypothesized conclusion $H$, followins from a premise, $P$
- Notation: $H|P$
    - $P(H|P)$ is the strength of the argument $H|P$

#### Mathematical model for inductive reasoning

- 'AND' rule: $P(A\hat B|P) = P(A|P)P(B|A\hat P) = P(B|P)P(A|B\hat P)$
- 'OR'  rule: $P(A\cup B|P) = P(A|P)+P(B|P)-P(A\cap P|P)$
- 'NOT' rule: $P(\bar{A}|P) = 1-P(A|P)$

### Interpreting PDFs

- **Frequentist Approach:** Describes the distribution of the RV across a sequence of trials. It is a limited version of a histogram.
- **Bayesian Approach:** Quantifies uncertainity in Inductive inferences about a particular case at hand. $p(x)$ describes now how $x$ is distributede, but how probability is distributed over the possible values $x$ might have taken iun the single case before us. It's a classical physics density function.

### Frequency and Probability
- **Bernoulli:** Bernoulli's weak law of large number: If P(success|...) doesn't change from sample to sample, it may be interpreted as the expected relative frequency.
    - $p(x;\mu,\sigma)$: $x$ is distributed as normal with mean...
- **Bayes:** If $P(success|...)$ doesn't change from sample to sample, it may be estimated using relative frequency data.
    - $p(x|\mu,\sigma)$: The probability for $x$ is distributed as normal with mean...

- Bayesian inference uses probability theory to quantify strength of data-base arguments

### Deriving results

**Likelihood:** It's incaopable of being integrated, because it is a function of $\mu$, but it denotes the probability of observing data given $\mu$
- A statistical model connects a parameter space to sample space.

#### Roles of probability
- **Frequentist:** Denies the legitimacy of pdf on the parameter space.
- **Bayesian:** Allows pdf over the parameter space (posterior distrbution)

### Bayesian and Frequentist approaches in parameter uncertainity estimation ---

**Frequentist:**
- A frequentist estimate of a $68\%$ confidence interval refers to the fact that if the experiment is conducted many times under the exact same conditions, the true value will lie in atleast $68\%$ of the intervals.

**Bayesian:**
- Given the data and the prior knowledge, there's a $68\%$ probability of the true value lying in the interval.
- It also means if I can draw multiple samples using the same prior, then my $68\%$ HPD region will contain the true value $68\%$ of time. 

---

## Probabilty theorems for data analysis

1. Bayes Theorem
2. Law of Total Probability:

- Consider exclusive and exhaustive ${B_i}$
$$
\sum_i P(A,B_i|C) = \sum_i P(B_i|C)P(A|B_i,C) = P(A|C)
$$

- Here, $C$ refers to the context.
- If we do not know how to get $P(A|C)$ directly, we can find a set of ${B_i}$ and use it as a basis to extend the conversation.
- This also means we can marginalize over $B_i$s, to take it out of the pitcutre.

## Inference with parametric models

- Models $M_i$ (i=1 to N), each with parameters $\theta_i$, each imply a sampling distribution. That is, if I know $\theta_i$ and $M_i$, I can get a $p(D|\theta_i, M_i)$

### Class of problems

**Single-model inference:** Inferring parameters of a single model
**Multi-model inference:** Either compare different models, or account for model uncertainities for constraining a parameter common to all the models.
**Model checking:** If a particular model is adequate?

