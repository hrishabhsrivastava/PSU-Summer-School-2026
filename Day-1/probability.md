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
**Random variable:** A function that pairs outcomes with numbers. It takes in real values. It's $\mathcal{F}:\Omega\rightarrow\mathbb{R}$

### Sample space
- Sample space for coin toss: $\Omega={H,T}$
- Each outcome is assigned a probability according to the physical understanding of the experiment.

#### Discrete Sample Space
- A finite or countably infinite sample space is sometimes called discrete.
- For an experiment with finite sample space $\Omega=\{o_1, o_2,...,o_m\}$, we assign a probability $p_i$ to the outcome $o_i$ for every $i$ in such a way that $\Sum p_i=1$

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
P(A\cup B) = = P(A) + P(B)
$$

### Probability Mass Function

It is a function that summarizes the possible non-zero values of $P(X=x)$, also denoted as $f(x)$ or $p(x)$ or $f_X(x)$

### Axioms of probability
1. $P(A)\geq 0$ (Non-negativity)
2. If $A$ is the whole sample space $\Omega$, then $P(A)=1$
3. If $A_1, A_2, ...$ are mutually exclusive (i.e., disjoint), then,

$$
P(\bigcup_{i=1}^\infty A_i) = \Sum_{i=1}^{\infty} P(A_i)
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
