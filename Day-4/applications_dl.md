# Diverse Astronomy Applications of Deep Learning (Ashish Mahabal, CalTech)

## Tips for data analysis
1. Prepare the data well
2. Abstract the data well.
3. In order not to find out trivial correlation, keep domain information or keep the contact scientist in loop

- If a problem can be solved by a simppler tool, like decision trees, it should be used over deep learning which cannot be explained well

- Ensemble of telescopes perform better by removeing biases of individual models.

## Multiclass classifiers

- It's often better to build several binary classifiers over a single multiclass classifier
    - Several binary classifiers classify an image into multiple categories.
    - We can then ask the experts what do they think about it, rather than giving it a class based on probability scores.

## Classifying spectra

- Classifying spectra using Deep Learning: Fremling et al. (arXiv: 2104.12980)
