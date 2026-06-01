# Introduction to AstroStatistics (Dr. Eric Feigelson)

## Role of statistics in astronomy

- Astrophysics is the study of the instrinsic nature of astronomical bodies and the processes by which they interact and evolve.
- Astronomy is the observational study of matter beyond Earth.

- **Statistics:** 
    - Statistics is the reduction of data (RA Fisher, 1922).
    - Mathematical body of science that pertains to the collection, interpretation or explanation and presentation of data (Wikipedia, 2014). This is more related to astrophysics.
    - A statistical inference carries us from observations to conclusions about the populations samples (DR Cox, 1958).


### Relating statistics to scientific models 
- All the models are wrong, but some are useful (Box and Draper, 1987). Box was Fisher's son-in-law.
- No need for hypothesis to be true, they should just yield calculations which agree with observations (CNR Rao). He was the last student of Fisher

- Astrostatistics is the bridge between observational astronomy to astrophysics. It's just modelling the observational data to understand the underlying physics. Astronomical research is just statistical inferencing.

### Recommended steps in the statistical analysis of scientific data
1. Exploration of data -- without a model. Just plot it and see if it has too many outliers, or it shows a pattern.
2. Careful statement of the scientific problem -- specify what exact science do I need out of this data.
3. Model formulation in mathematical form -- a model with parameters
4. Choice of statistical method(s) -- like least squares regression or maximum likelihood, for example.
5. Calculation of statistical quantities -- minimize $\chi^2$ or maximise the likelihood. *R* is the language of statistician, used for this purpose.
6. Judicious scientific evaluation of the results -- back to the definition of statistics, about what we learnt from the data.

### Extra tips
- Prefer non-paramteric and scale-invariant quantities, and try multiple methods.
- Statistics is only a tool towards understanding nature from incomplete information.

## History of statistics in astronomy
- Astronomers and statisticians were the same people in the most of the history.
- **Ancient Greeks to 18th century:** Best estimate of the length of an year to plant crops.
    - Middle of range: Hipparcos (4th century BC)
    - Observe only once! (medieval)
    - Mean (Brahe in 16th C, Galileo in 17th C and Simpson in 18th C)
    - Median with Bootstrap (21th C), because mean assumes a pure Gaussian distribution.

- **19th century:** Observation of planets to estimate orbital parameters using Newtonian mechanics
    - Legendre, Laplace and Gauss developed least squares regression and normal, i.e. Gaussian, error theory(~1800-1820)
    - Gauss was a director of an astronomical observatory
    - Prominent astronomers contributed more (~1850)

- **Lost century:** The field of statistics and astronomy moved away from each other due to
    - Statistician realized other fields could use statistics, like agriculture, mining, manufacturing.
    - Astronomers realized there's more Physics, like relativity, electromagnetic theory, etc than Newtonian gravity to learn and use.

- Astrostatistics isn't so good in the modern astronomical studies, because we do not use all the statistics developed by statisticians. We confined it to narrow mathods:
    - Fourier transform
    - Least squares regression
    - Kolmogorov-Mirnov good-of-fit
    - PCA

- We also misuse traditional statistical methods without realizing their limitations.

**Textbook:** Modern Statistical Methods for Astronomy (by Fiegelson and Babu)

- Modern cosmology requires a whole lot of statistical methods, like for example strong lensing needs the knowledge of shape statistics.

**Astroinformatics:** To treat massive data streams and databases. It involves perforfming computationally intensive astronomy and might require parallel computing.

 `Statistics guides the sicentist on what to compute. Informatics helps the scientist perform the computation.`


