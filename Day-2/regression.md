# Regression (Dr. Ashley Villar, Harvard)

## Introduction

**What is regression?** Regression aims to construct a model that relates the response variable $Y$ to the predictor variables $X_1, X_2,...,X_p$

## Regression using MOO
1. **Model:** To fit the Physics
2. **Objective Function:** A metric to quantify how well the model fits the data
3. **Optimization Method:** Used to find the optimal model

## Linear Regression

$$
Y = \beta_0 + \beta_1X_1 + \beta_2X_2 + ... +\beta_pX_p + \varepsilon
$$

- The available sample used for fitting is referred to as **training set**

_ The following is also linear regression:

$$
Y = \beta_0 + \beta_1X + \beta_2X^2 + \beta_3X^3 + \varepsilon
$$

### The error term

- $\varepsilon$ is called an irreducible error. It is a random error which we do not aim to remove completely, otherwise it would lead to 'overfitting'.
- It is often assumed to be Gaussian $\varepsilon\sim\mathbb{N}(0, \sigma^2)$
- If it changes as a function of data, it's called 'heteroskedastic'.
- We will assume that the errors are IID and uncorrelated.

### Fitting

- **Parameters:** The parameters of our model are $(\beta_0, \beta_1, \varepsilon)$
- **Objective function:** We use least squares regression:

$$
\sum_{i=1}^n (Y_i - (\beta_0 + \beta_1X_i))^2
$$

- Least squares regression minimizes the residuals

- **Optimization**: We need a method which is computationally efficient and accurate.
    - Possibilities: 1. Random guess
                    2. Follow an algorithm
                    3. Solve analytically

    - We find a global minimum analytically:

$$
\hat{\beta}_1 = \frac{\sum_{i=1}^n (X_i - \bar{X})(Y_i - \bar{Y})}{\sum_{i=1}^n (X_i - \bar{X})^2}
$$

$$
\hat{\beta}_0 = \bar{Y} - \hat{\beta}_1\bar{X} 
$$

### Correlation Coefficient
- The Pearson correlation coefficient tells the relation betwwen two variables.
- **Covariance:**

$$
{\rm Cov}(X, Y) = \sum_{i=1}^n (X_i - bar{X})(Y_i - \bar{Y})/(n-1)
$$

- **Correlation:**

$$
r_{xy} = {\rm Cov}(X, Y)/s_xs_y
$$

    - $s$ denotes sample standard deviation

### Coefficient of Determination

-  It explains the scatter of the fit
- $R^2$ is not designed to show the quality of the fit

$$
R^2 = 1 - \frac{\sum_i (Y_i - \hat{Y}_i)^2}{\sum_i(Y_i - \bar{Y})^2}
$$

### Residual as a diagnostic tool

- Since we can't use $R^2$, we can use residualsas a diagnostic tool.
- If our model is a reasonable fit, the residuals should be a reasonable estimate of $\varepsilon$, the irreducible scatter.

## Logistic regression
- Used to model a discrete outcome in a classification problem.
- Logistic regression can mdoels discrete output

$$
P(Y=1|X) = \frac{1}{1+\exp(w_0+\sum_i w_iX_i)}
$$

$$
P(Y=0|X) = 1 - P(Y=1|X)
$$

### Objective Function

- We define a cross-entropy function:

$$
H(P*|P) = -\sum_i P*(i)\logP(i)
$$

- $P*(i)$ is the true class distrbution
- $P(i)$ is the predicted class distribution

### Optimization
- The best option is to use an algorithm, like gradiaent descent or MCMC.

## Model Selection

- Including too many predictors leads to overfitting.
- Extra predictors will always decrease residuals and $R^2$, so they are not useful.
- Complexity leads to loss of generalizability.

**Idea:**
- Split the data into training and test set.
- Use the test set to find hyperparameters, i.e., number of parameters.

### Leave-one-out cross-validation
- Imagine fitting a model, for each observation $i$, which "leaves out" that observation and fitting the model to the remaining set.
- The fit model is then used to predict the response for observation $i$.
- We can track the response of the model for observation $i$ and compile it all into a score

$$
LOOCV = \frac{1}{n} \sum_i (Y_i - \hat{Y}_{-i})^2
$$

### Confidence and Prediction Intervals

- We aim to measure the uncertainity of the prediction.
- Two inference objectives:

1. **Making predictions:** I have a 'prediction interval' for new values of $Y$ when I am trying to make predictions. For example, finding photometric redshifts.

2. **Characterizing relationships:** Needs a confidence interval on the regression functions (i.e., the parameters)

- For large $n$, $95\%$ prediction intervals have a half-width which is approximately $2\sigma$ (when we can assume it to be Gaussian, cz of Central Limit Theorem).

## Non-parameter regression
- In a parametric regression, the contribution to the estimate from the assumptions is fixed (i.e., a known functional form)
- In a non-parametric model, we use the data without a functional form using a smoothing parameter $h$.

### Local linear regression

- We assume that the relation is only locally described by a linear relationship
- **Steps:**
    1. Pick a local $x_0$
    2. Create a neighbourhood around $x_0$, using the parameter $\alpha$, often called as the 'span' of the data.
    3. Weigh the data in the region: the points closer to $x_0$ should receive higher weights, but the ones farther away should recieve less weights (**Why?**)
        - It can be done using the **tri-cube weight function:**
        $$
               w_i=
                \begin{cases}
                (1-|\frac{x_i-x_0}{\rm max.dist}|^3)^3 & \text{, if $x_i$ in the neightborhood of $x_0$}\\
                0 & \text{if $x_i$ isn't in the neighborhood of $x_0$} 
        $$
    4. Fit a local regression line.
    5. Estimate the regression function in that window $f(x_0)$

### Smoothing parameter selection
- A smaller value leads to rougher estimate, a larger value leads to 'smoother' estimate.
- We can optimize it using cross-validation

### Smoothing spline

- It's another non-parameteric method.
- It uses a piecewise function.
- We can have knots for slope change.
-Only the highest order coefficients change at each knot.

**Notes:**
- In astronomy, we only use non-parameteric model, when we are only interested in predictions, or we want to see the trend in data.
