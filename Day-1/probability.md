# Laws of Probability (by David Hunter)

**Blindsight and visuo-spatial neglect**
 A patient, P.S., had sustained right cerebral damage. She was presented simultaneously with two frawings of a house. She judged the drawings to be identical, yet when asked to select which one to live, she *reliably chose* the house wasn't burning.

- This appeared in a Nture article.
- She chose the non-burning house 14 times in 17 trials. It's statistically convincing. One can perform a 'calculation' to get to a number.
- When data are collected under nearly identical conditions, the measurement consists of variations. It thus needs statistical analysis.

## Why study probability?

### Do random phenomena exist in Nature?
- Is coin flip random? Not really, if given enough enough information. Modelling the outcome as random gives a parsimonious representation of reality.
- Randomness isn't total unpredictability. It's predictable unpredictability.
- If mathematics and probability were well understood in the past, deterministic models (like the trajectory of a planet) could've been be found using probability.

### Existence of uncertainity
1. Our inability to observe accurately all the inputs required to compute the outcome;
2. Excessive cost of observing all the inputs;
3. Lack of understanding the phenomenon;
4. Dependence on choices to be made in the future, like the outcome of an election.

- Probability gives us a way to model uncertainity, i.e., to provide it a mathematical structure.

## Mathematical formalization
**Random variable:** A function that pairs outcomes with numbers. It takes in real values. It's $\mathcal{F}:\Omega\to\mathbb{R}$

### Sample space
- Sample space for coin toss: $\Omega={H,T}$
- Each outcome is assigned a probability according to the physical understanding of the experiment.

#### Discrete Sample Space
- A finite or countably infinite sample space is sometimes called discrete.
- For an experiment with finite sample space $\Omega=\{o_1, o_2,...,o_m\}$, we assign a probability $p_i$ to the outcome $o_i$ for every $i$ in such a way that $\sum p_i=1$

### Event
- A subset $E\subseteq\Omega$ is called an event. This is the mathematical definition of an event in case of an discrete sample space.
- If $\Omega$ is uncountably infinite, we cannot allow arbitrary subset to be called events, we can only allow a **measurable subset**.
- A **probability space** consists of:
    - A sample space $\Omega$,
    - A set $\mathcal{F}$ of subsets of $\Omega$ that will be called the events,
    - a function $P$ that assigns a probability to each event and that must obey certain axioms. The probability should sum up to 1.
- Random variables can be used to define an event.
- The probabilistic properties of a random variable are determined by the probabilities assigned to the outcomes of the underlying sample space.

### Disjoint events
- Probability of unions = sum of probabilities. For disjoin events $A$ and $B$,

$$
P(A\cup B) = P(A) + P(B)
$$

### Probability Mass Function

It is a function that summarizes the possible non-zero values of $P(X=x)$, also denoted as $f(x)$ or $p(x)$ or $f_X(x)$

### Axioms of probability
1. $P(A)\geq 0$ (Non-negativity)
2. If $A$ is the whole sample space $\Omega$, then $P(A)=1$
3. If $A_1, A_2, ...$ are mutually exclusive (i.e., disjoint), then,

$$
P(\bigcup_{i=1}^\infty A_i) = \sum_{i=1}^{\infty} P(A_i)
$$

- If $\Omega$ is uncountably infinite, it is impossible to define $P$ satisfying these axioms if "event" means any subset of $\Omega$. It's because any single outcome has probability $0$, but axiom 2 states their sum to be $1$.

### Inclusion-Exclusion Rule
- For two events $A$ and $B$

$$
P(A\cup B) = P(A) + P(B) - P(A\cap B)
$$

- This can be generalized to any number of events, $n$.

- When $\Omega$ has $m$ equally likely outcomes,

$$
P(A) = \frac{|A|}{|\Omega|}=\frac{|A|}{m}
$$

## Conditional Probability
- For events $A$ and $B$, the probability that $A$ occurs given that $B$ occurs is called the conditional probability of $A$ given $B$ and is written as $P(A|B)$.
- **Independent events:** If $A$ and $B$ are independent, $P(A|B) = P(A)$

$$
P(A|B) = \frac{P(A\cap B)}{P(B)}
$$

- In other words, we are in the sample space of $B$. Hence, we scale everything by $P(B)$.

### Multiplicative law of conditional probability

$$
P(A\cap B) = P(A|B)P(B)
$$

### Birthday Problem

What is the probability that, in a group of $n$ people, there is at least one pair of matching birth dates?

_ Assuming independent birthdays,

$$
P = 1 - \frac{365}{365}\times\frac{364}{365}\times\frac{363}{365}...n\text{ terms}
$$

- This can also be written as,

$$
P(A_1^c)\times P(A_2^c|A_1^c)\times P(A_3^c | A_1^c,A_2^c)\times ...
$$

where, $A_i$ refers to the matching birthdays for $i$ people.

### Partitioning the sample space
- It means creating a set of non-overlapping events, such that their union gives the whole sample space.
- Let $B_1,...,B_k$ be a partition of a sample space $\Omega$ and let $A$ be an arbitrary event.

$$
P(A) = P(A\cap B_1) + ... + P(A\cap B_k)
$$

This is called the **Law of Total Probability**

**Doubt:** Why isn't the probability of getting Heads in the example of the Law of Total Probability equal to 7/12, i.e., $\frac{n_H}{N_H+n_T}$

### Bayes' Theorem

$$
P(B_i | A) = \frac{P(A|B_i)P(B_i)}{P(A)} = \frac{P(A|B_i)P(B_i)}{\sum_{j=1}^m P(A|B_j)P(B_j)}
$$

- Named after Thomas Bayes.
- Some paradoxes: Monty Hall problem, Three-card problem, 

### Independence

$$
P(A\cap B) = P(A)P(B)
$$

- This isn't trivially defined for more than two events.
- We define 'mutually independent' events.

## Discrete random variables

### Expectation of a R.V.
- Expectation is a weighted average

$$
\mu = E(X) = \sum_{i=1}^n P(X=x_i)
$$

- If $Y=g(X)$, i.e., a new RV which is a function of the original RV,

$$
E(Y) = E[g(X)] = \sum_{i=1}^n g(x_i)P(X=x_i)
$$

### Variance of a RV

$$
\sigma^2 = {\rm Var}(X) = E[(X-\mu)^2]
$$

- Expectation is a linear operator

$$
E(aX + bY) = aE(X) + bE(Y)
$$

- Using Cauchy-Schwartz inequality, which states that the expectation of the square must be greater than the square of the expectation, we can show

$$
E[(X-\mu)^2] = E(X^2) - \mu^2
$$

- Variance conveys the spread of the random variable around its mean.

**Doubt:** How is the square of the random variable constant in the example on variance measures speed?

- Not all random variables has an expectation, like for example, a Cauchy Distribution.

### Binomial RV
- Consider $n$ independent trials where the probability of "success" in each trial is $p\in (0,1)$. Let $x$ denotes the totla number of successes,

$$
P(X=x) = {n\choose x} p^x(1-p)^{n-x}
$$

- The expectation $E(X)=np$ and the variance ${\rm Var}(X)=np(1-p)$
- For independent random variables, the variance of the sum is the sum of the variance.

### Poisson RV
- Consider a random variable $Y$, such that for some $\lambda>0$

$$
P(Y=y) = \frac{\lambda^y}{y!}e^{-\lambda}
$$

- Here $E(Y)=\lambda$ and Var $(X)=\lambda$

- A Binomial RV with very high $n$ and very low $p$, can be modelled as a Poisson RV with $\lambda=np$

- The Poisson has this constraint that mean and variance should always be the same. Don't use Poisson, if it isn't!

### Geometric RV

- The goal is counting failures before the first success.
- Consider independent trials where the probability of success is $p$. Let $X$ denotes the number of failures before the first success.

$$
P(X=x) = (1-p)^xp
$$ 

- It has $E(X)=\frac{q}{p}$ and Var $(X)=\frac{q}{p^2}$ where $q=1-p$.

### Negative Binomial RV

- Number of failures before $r$th success.

$$
P(X=x) = {r+x-1\choose x}(1-p)^x p^r
$$

- It has $E(X)=\frac{rq}{p}$ and Var $(X)=\frac{rq}{p^2}$

- Negative binomial is used to model count data more often, because it doesn't have the constraints of Poisson.

## Continuous distributions

### Technical issues
- If $\Omega$ is uncountably infinite, the previous definition of the random variable won't work.
- **Definition:** A function $X:\Omega\to\matbb{R}$ is said to be a random variable iff for all real numbers $a$, the set {\omega\in\Omega: X(\omega)\leq a} is an event.

### Beyond discreetness

- The cumulative distribution function $F(x)$ is defined as,

$$
F(x) = P(X\leq x)
$$

- The probability density function $f$ is defined as,

$$
F(x) = \int_{-\infty}^x f(t)\,dt
$$

- $\lim_{X\to-\infty}F(x)=0$ and $\lim_{X\to\infty}F(x)=1$
- Note that while CDF is uniquely defined, the same isn't true for PDFs. One CDF can have multiple possible PDFs.

### Exponential R.V

- It is the continuous version of geometric.
- Let $\lambda>0$ be some positive parameter. The exponential distribution with mean $1/\lambda$ has density

$$
f(x) = 
\begin{cases}

\lambda\exp(-\lambda x) & \text{if } x \geq 0 \\
0 & \text{if } x < 0

\end{cases}

$$

- The CDF would look like,

$$
F(x) = \int_{-\infty}^x f(t)\,dt
\begin{cases}
1-\exp(-\lambda x) & \text{if } x>0 \\
0 & \text{otherwise}
\end{cases}
$$

### The Normal Distribution

$$
f(x) = \varphi_{\mu,\sigma^2} = \frac{1}{\sqrt{2\pi}\sigma}\exp(-\frac{(x-\mu^2)}{2\sigma^2})
$$

- The CDF is represented by $\Phi$

### The Lognormal Distribution

- If $X\sim\mathbb{N}$, then $\exp(X)$ has a lognormal distribution with parameters $\mu$ and $\sigma^2$.

$$
f(x) = \frac{1}{x\sigma\sqrt{2\pi}}\exp(-\frac{(\ln(x)-\mu^2)}{2\sigma^2})
$$

- Only for $x>0$
- Used when parameters are in the multiplicative scales.

### Expectation
- For a random variable $X$ with density $f$, the expectation value of $g(X)$ will be

$$
E[g(X)] = \int_{-\infty}^\infty g(x)f(x)\,dx
$$

- The variance of $X$ is given by,

$$
\sigma^2 = E[(X-\mu)^2] = \int_{-\infty}^\infty (x-\mu)^2f(x)\,dx = \int_{-\infty}^\infty x^2f(x)\,dx - \mu^2
$$

- For a lognormal distribution,
$$
E(X) = e^{\mu + (\sigma^2/2)}
$$

- Note that variance isn't a linear operator.

## Limit Theorems

- Behaviour of sums as $n\to\infty$.
- **IID**: If the experiment never changes and the result of one experiment no not influence the results of any other, this sequence of experiments is called independent and identically distributed.
- For a large number of samples, as the sample size increases, the sample mean exhibits a normal distribution.
