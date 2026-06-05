# A Conceptual Introduction to Deep Learning (Dr. Joshua Speagle, UToronto)

## Linear Regression

After fitting a linear regression model, we carry out predictions for new data points $x^*, y^*$. Thus,

$$
\hat{y}^* \sim \mathbb{N}(\hat{A}x^*,\sigma^2+x^*\Sigma_Ax^*)
$$

- $\hat{y}^*$ is the prediction of $y^*$ from the data $x^*$
- Since $\hat{A}$ ios an estimator of the true parameter vlue, we will add the covariance term $\Sigma$ to the original uncertainity $\sigma^2$

## Neural Networks

- As the number of parameters (weights and biases) increases to infinity, each parameter gets infinitesimally updated by the new data.
- It depicts an asymptotic behaviour
- Thus in deep neural networks, the architecture starts mattering more than individual weights and biases

### Convolutional and Pooling layers.

- To get the final classification of an image, the feature learning is done by a series of convolution and pooling layers
- The classification is done by a flattened **perceptron**.

### Attention and Transformers

- In simple words, it's a way to figure out how much do we want one thing to be related to/to affect the rest of the thing in a neural network.
- It's good for long-range interactions.

### Initialization

- Initialization of weights is extremely important in an overparameterized world.
- It helps prevent 'vanishing gradients' and 'exploding gradient' problems
- Critical initialization ensures fast learning 

### LR and Batch-Size

- **Large Learning Rates:** Large eigenvalue directions of the gradient
- **Small batch sizes:** Large eigenvalue directions of the gradient covariance across the data

**RULE OF THUMB:** learning rate / batch size $\sim$ constant!
