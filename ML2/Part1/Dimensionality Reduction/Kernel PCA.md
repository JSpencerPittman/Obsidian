# Kernel PCA
Good at preserving clusters of instances after projection, or some times even unrolling datasets that lie close to a twisted manifold. 

### Selecting a kernel and tuning hyperparameters
A decent way is to train a classifier on different dimensionality reduction kernels. 
Although some data can become infinite dimensional its hard to use reconstruction error, 
so we use a pre-image which is part of the original dataset. 
1. Approach is to train a supervised regression model with the project instances as the training set and the original instances as the targets.
> fit_inverse_transform=True to accomplish this

previous:
[[PCA]]
next:
[[LLE]]