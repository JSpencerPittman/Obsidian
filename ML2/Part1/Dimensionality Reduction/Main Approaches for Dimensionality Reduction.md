# Main Approaches for Dimensionality Reduction
### Projection
In most real-world problems training instances aren't spread out uniformly across all dimensions. Many features are near constant, while others are highly correlated, As a result all training instances lie within a much lower-dimnesional subspace of the high-dimensional space. 

However in the case of a swiss-roll dataset where unrolling would be ideal this approach fails. 

### Manifold Learning
The swiss roll is an example of a 2D manifold
A 2D manifold is a 2D shape that can be bent and twisted into a higher dimensional space.
More generally a d-dimensional manifold is part of an n-dimensional space.

Manifold learning is modeling the manifold on which the training instances lie. It relies on the *manifold assumption*, also called the *manifold hypothesis*.

### Manifold Hypothesis
Most real-world high-dimensional datasets lie close to a much lower-dimensional manifold.
Often empirically observed. 
For example shuffling an 24x24 image would only resemble a digit in very few instances narrowing the degrees of freedom available. 
Another assumption is that the task at hand will be simpler if expressed in the lower-dimensional space of the manifold. So sometimes speeding up the training will increase the decision boundary's complexity.

previous:
[[Curse of Dimensionality]]
next:
[[PCA]]