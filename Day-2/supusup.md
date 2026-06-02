# Supervised and Unsupervised Learning

**Unsupervised**
- Clustering
- Feature selection
- Dimensionality reduction

**Supervised Learning**
- Classification
- Regression
- Forecasting

## Unsupervised Learning
Learning structures in our data.

### Dimensionality Reduction
- Reducing the amount of information we need to caputre this dataset
- The idea to represent the same data in a latent space - it doesn't have to be physical.

**What can we do in a low-dimensional space?**
1. Better feature selection for classification: might notice clustering
2. Anomaly detection: might find an data point in a region it's not supposed to be at
3. Data simulation
4. Physical interpretability: a little rare

**Doubt:** Sounds to me like the latent space is a space of parameters. So, all we are doing is parameter fitting?

#### How to do it without fitting?
- Break it down into basis vectors
- Choose the basis vector as the eigenvector along the direction of the maximum variance

#### Principal Component Analysis
1. Find the eigenvectors of the dataset
2. Sort the eigenvectors by explained variance
3. Project the data onto each basis, tracking the weights

**Power Iteration Method**
It can be computationally expensive to find every eigenvector if our data-space is high dimensional. We follow the following algorithm instead:
1. Given $M=X^TX$, select a random vector $v_0$
2. For $i=1, 2, 3, ...$, let $v_i=M_iv_0$
3. If $v_i/|v_i|\sim v_{i-1}/|v_{i-1}|$, then $v_i/|v_i|$ is our first component.
4. If not, repeat steps 1-3 until the condition is met.
5. Project the data orthogonally to $w_1$. Repeat the procedure to fing the next PCA component and so on.

- Note that PCA can remove structures in our data, if it doesn't lie along the the principal components.

#### t-SNE

- It refers to t-distributed stochastic neighbor embedding.

**Neighbor embedding**
- It refers to actually identifying the neighbours in the original high dimensional space.
- Neighbourhood can be calculated using Euclidean distances

$$
p_{i|j} \propto \exp(-\frac{||x_i-x_j||^2}{2\sigma_j^2})
$$  

- t-SNE aims to learn an embedding which preseves distance measures in latent space.
- It uses a Student $t$-distribution
- Measure $p(x_i|x_j)$ in the observed space, which is Gaussian and $q(x_i^'|x_j^')$ in latent space, which is the Student's $t$ distribution. (WHY?)
- Use KL Divergence to minimize the pdfs $p$ and $q$
- It's stochastic because we start with choosing random points.

**Perplexity:** It is a hyperparameter, which means the number of points in a cluster.

### Clustering
Just answering if I see clusters in the data

#### Gaussian Mixture Models
The clusters are assumed to be Gaussians

$$
p(x|\Theta) = sum_{k=1}^K \alpha_kp_k(x|\mu_k, sigma_k)
$$

- Note that $k$ is a hyperparameter. 

**Membership weights:** The probability that $x_i$ comes from the $k$th component

$$
w_{i,k} = \frac{\alpha_kp_k(x_i|\mu_k, \sigma_k)}{\sum_{m=1}^K \alpha_kp_m(x_i|\mu_m, \sigma_m)}
$$

- This idea can be easily extended to hgigher dimensions.

**Objective function:** Log-likelihood

$$
\sum_{i=1}^N (\log\sum_{k=1}^K\alpha_k p_k(x_i|\mu_k, \sigma_k))
$$

**Optimization**
- It's very hard to take the gradient of the log-likelihood objective function, hence gradient descent is not used.
- We use Expectation-Maximization

**Expectation Maximization (EM) Algorithm**
1. Choose a random set of parameter values ($\theta$) whcih satisfies our constraints
2. **E-Step:** Compute the probability matrix: the probability of each point belonging to each cluster ($w_{ik}$'s)
3. **M_Step:** Calculate new parameter values - 

$$
N_k = \sum_{i=1}^N w_{ik}
$$

$$
\alpha_{\rm new} = \frac{N_k}{N}
$$

$$
\mu_k^{\rm new} = \frac{1}{N_k}\sum_{i=1}^N w_{ik}x_i
$$

$$
(\sigma_k^2)^{\rm new} = \frac{1}{N_k}\sum_{i=1}^N (x-\mu)^2
$$

4. Repeat it multiple times until it converges.

#### K-Means Clustering
- I assume the presence of $k$ clusters. My goal is to find the cluster centers.
- **Model:** $\Theta={\mu_1, mu_2,...,\mu_k}$
- **Objective:** $\sum_{i=1}^N\min_{c_k\in C}(||x_i-\mu_k||^2)$
- **Optimization:** Using EM
    - Choosen random cluster centers
    - E-step: calculate distances from the cluster centers
    - M-step: assign the least distant cluster as home, then re-calculate the cluster center.
    - Repeat the steps until convergence.

## Supervised Learning
- I know the answers for a training set and I want to train an algorithm to give me the same quantity for an unseen sample.

### Classification: Support Vector Machine

- The goal is to find a decision boundary (a line or a hyperplane) for different classes in the parameter space.
- Ideally, I need three points to define two parallel planes which separte the classes. These are called as **Support Vectors**.
- Mathematically, we can define the perpendicular plane to the street and the distance along this vector.

$$
\vec{x}_i\cdot\vec{w} + b \geq + 1
$$

$$
\vec{x}_i\cdot\vec{w} + b \leq -1
$$

- This is how the two classes could be defined. We want to maximize the width of the street while subject to the two inequality constraints listed above.

**Important for the objective function**
1. Should only depend on the support vectors
2. Should be differentiable (thus, we can use gradient descent)
3. The objective should only depend upon the dot product between pairs of support vector.

**Non-linear decision boundary**
- We change the parameter space mathematically to some $\Phi(x_i)$, in order for the decision boundary to become linear again.
- We don't need to find the whole $\Phi(x)$ again, since decision boundary only depends upon support vectors.
- We, thus define a Kernel function,

$$
K(x_i, x_j) = \phi(x_i)\cdot\phi(x_j)
$$

- One example of Kernel function is the Gaussian Kernel,

$$
K(x_i, x_j)= \exp(-\frac{||x_i-x_j||^2}{2\sigma^2})
$$ 

### Classification: Decision Trees
- A decision tree makes a series of binary cuts to sort data

**Some terminology**
- Nodes: Junctions in a tree
- Leaves: Represents the final outcome

**Random Forest:** Combines a series of decision tree to determine the final outcome.

#### Model
- A series of set of decision trees which attempt to classify a set of objects, i.e., a random forest

#### Objective
- **Gini Impurity:** Used to choose a decision boundary

$$
1-\sum_k^K p_k^2
$$

- Our objective function is the weighted Gini Impurity.
- We find a decision boundary inside a tree by minimizing the weighted Gini Impurity.
