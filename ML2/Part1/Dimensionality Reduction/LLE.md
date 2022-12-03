# LLE
Locally Linear Embedding
Another nonlinear dimensionality reduction (NLDR) technique

Manifold technique that doesn't rely on projections
Works by measuring how each training instance linearly relates to its closest neighbors and then looking for a low-dimensional representation of the training set where these local relationships are best preserved. Very good at unrolling manifolds where there's not much noise. 

For each training instance $x^{(i)}$ the algorithm identifies its $k$ closest neighbors then reconstructs $x^{(i)}$ as a linear function of these neighbors. Trying to find the weights $w_{i,j}$ such that the squared distance between $x^{(i)}$ and $\sum^m_{j=1}w_{i,j}x^{x^{j}}$ is the smallest possible where $w_{i,j}=0$ if $x^{(j)}$ is not one of the neighbors. 

*Equation 8-4. LLE step one: linearly modeling local relationships*
$$\LARGE\begin{align}
&\hat W=\underset{w}{argmin}\sum^m_{i=1}(x^{(i)}-\sum^m_{j=1}w_{i,j}x^{(j)})^2\\
&\text{subject to }w_{i,j}=0\text{ if }x^{(j)}\text{ is not one of the k neighbors of }x^{(i)}\\
&\text{subject to }\sum^m_{i=1}w_{i,j}=\text{ for i = 1, 2, ..., m}
\end{align}$$
> $\hat W$ matrix holding all local relationships

How do we map it to d-dims while preserving the local relationships.
If $z^{(i)}$ is the image of $x^{(i)}$ in d dimensions then we want the squared distance between $z^{(i)}$ and $\sum^m_{j=1}\hat{w}_{i,j}z^{(j)}$ 
Now instead of keeping the instances fixed and finding the optimal weights we are doing the reverse: weights are fixed and finding the optimal positions.

*Equation 8-5. LLE Step two: reducing dimensionality while preserving local relationships*
$$\LARGE\hat Z=\underset{Z}{argmin}\sum^m_{i=1}(z^{(i)}-\sum\hat w_{i,j}z^{(j)})^2$$
> $Z$ is the matrix containing all $z^{(i)}$ 

This runs in $O(mlog(m)nlog(k))$ for finding k nearest neighbors, then $O(mnk^3)$ for optimizing the weights, and $O(dm^2)$ for constructing the low-dimensional representations. The $m^2$ means this algorithms scales poorly for large datasets.

previous:
[[Kernel PCA]]
next:
