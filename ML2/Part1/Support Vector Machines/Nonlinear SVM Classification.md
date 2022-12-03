# Nonlinear SVM Classification
One approach for unlinear datasets is to simply add more features. Which in some cases results in a linearly seperable dataset. Here's where the problems arise.

At a low degree the model can't fit complex datasets
At a high degree the model takes too long to load

A kernel trick makes it seem you have a miracolous amount of degree without actually having them. 

## Similarity Features
Another approach to tackle nonlinear problems is to add features using a computer similarity function. Which measures how much each instance resembles a particular landmark. 

Gaussian Radial Basis Function
$$\LARGE\phi_\gamma(x,\ell)=exp(-\gamma||x-\ell||^2)$$

The simplest approach for selecting landmarks is selecting every training instance as a landmark however the downside is this creates an overabundance of features. 

The hyperparameter gamma makes the similarity bell shape curve increasing irregularity of the dataset. 

**Scikit-Learn classes for SVM classification**
Class | Complexity | Out-of-core support | scaling required | kernel trick
-- | -- | -- | -- | --
LinearSVC | O(m x n) | No | Yes | No
SGDClassifier | O(m x n) | Yes | Yes | No
SVC | O($m^2$ x n) to O($m^3$ x n) | No | Yes | Yes