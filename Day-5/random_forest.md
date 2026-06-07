# Random Forest (Dr. Peter Freeman, CMU)

- (opinion) There's no such thing as "algorithmic bias". An algorithm is an algorithm!
- Selection bias refers to carefully selecting data to get particular results.

- Deep Learning needs a large amount of data. Hence, don't use it if the dataset is about ~1000-5000. It has too many parameters to tune, hence, it'll not work well.

**Limitation of Trees:**
- Tree algorithm is greedy:
    - If one predictor has more power, the split will always be made along its line, even when it misses out on some of the other important properties!

## Random Forest

Random forest adds two tweaks on the top of the base tree algorithm:
- New training data for each tree are created through bootstrapping, i.e., resampling the observed data with replacement ('bagging')
- Only a subset of predictor variables are considered.

### Tips
- Any number bigger than 100 for the number of trees.
- If the dataset is very large, then cut down on the number of trees to save on computation time, but even in that case, don't cut it down less than a 100!

## Boosting

- Can you aggregate multiple simple models to create a model that is more complex, but also has better predictive capabilities?
- The idea is to model the data using a simple model (a single split decision tree, i.e., a stump), pick out the residuals and model them using another stump, pick out these new residuals, model another stump, and so on...
- Boosting is an meta-algorithm. It applies another algorithm iteratively.
- It's not a tree algorithm, it can be applied on another algorithm.
- It helps grow a single tree 'slowly', rather than a whole forest!
- Both boosting and random forest helps to measure variable importance. 
