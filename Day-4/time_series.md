# Time Series Analysis (Dr. Eric Fiegelson, PSU)

Time series calculations are used in multiple domains, including astronomy, for predictions

## Important terminology

**Autocorrelation**
- ACF is a function of lag.
- The measured levels at a time $t_0$ depends on the measurements at a previous time.
- If the signal extends to large $k$ (i.e., lag), it's called a long-term memory. This includes red noise.
- White noise is exhibited by uncorrelated time series.

## Non-paramteric time-domain methods

1. ACF:
    - Partial ACF: All the mid-values (i.e., apart from $x_1$ and $x_k$) are ignored and removed.
2. Density estimation on time series using KDE, local regression, etc.


