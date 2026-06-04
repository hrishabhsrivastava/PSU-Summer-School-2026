# Spatial Model Statistics (by Dr. Murali Haran, PSU)

## Types of spatial models

### Spatial Point Process Data example

- **Swedish pines:** Totally random
- **Longleafs:** Marked point process, has both location, and a feature, both random 

## Spatial point process modelling

SPatial Point Processes can be modelled by specifying 
- A completely deterministic intensity function: A function of $\lambda(s)$
- A stoachstic $\lambda(s)$: draw it from a pdf, but remember that we only have one realization of such a stochastic process.

- Poisson process is a basis for point process, exactly how Gaussian is for a continuous random variable.

### Poisson process

 Remember that

- The intensity measure $\Lambda(A)=E(N(A))$
- The intensity function, $\lambda(s)$ is defined as,

$$
\Lambda(A) = \int_A \lambda(s) ds
$$

- $N(B)\sim$ Poisson($\Lambda(B)$)

## Ripley's $k$ function

- Refers to the the mean number of events within a distance $d$ for an event.
- Quantifies clustering
- The simplest method is to draw a circle of radius $d$ around every point, and count the number of points inside the circle and taken an average of it.

## Continuous-domain/geostatistical data

- These techniques aren't encountered as frequently in astronomy, except for approximating complex computer models:
    - Given how computer model behaves at a few set of inputs, approximate how the model would will behave at other input settings
    - The of geostatistical data in a conitnuous domain helps us explore even that part of the domain which doesn't necessarily have data, but it could.
    - Imagine all the empty spaces in the parameter space.
 
