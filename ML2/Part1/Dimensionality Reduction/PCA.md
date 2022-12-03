# PCA
principal component analysis
First identifies the hyperplane that lies closest to the data and then it projects the data onto it

### Preserving the Variance
Before projection you first need to choose the hyperplane
The better a line fits the data the wider its variance
So choosing the line that maximizes variances is usually best
In other words the line that reduces MSE is often best.

Often in choosing an axis PCA will find a second axis orthagonal to the first to account for the remaining variance. The ith axis is called the *ith principal component*(PC) of the data

For each Principal component, PCA finds a zero-centered unit vector point in the direction of pc

How do you find the PC's of a training set?
A standard matrix factorization technique called *Singular Value Decomposition (SVD)* that can decompose the training set matrix $X$ into the matrix multiplication of three matrices 
$$\LARGE X \rightarrow U\Sigma V^T$$
> $V$ contains the unit vectors that define all the principal components that we are looking for. 

*Equation 8-1. Principal components matrix*
$$\LARGE V=\begin{pmatrix}
\vert & \vert &  & \vert\\ 
c_1 & c_2 & \cdots & c_n \\ 
\vert & \vert & & \vert
\end{pmatrix}$$
MAKE SURE TO CENTER THE DATA

### Projecting down to d dimensions
Project it onto the hyperplane containing the first d principal components. 
To get the reduced dataset $X_{d-proj}$ of dimensionality $d$. Compute the matrix multiplication of the training set matrix $X$ by the matrix $W_d$ defined as the matrix containing the first $d$ columns of $V$ as shown below

*Equation 8-2. Projecting the training set down to d dimensions.*
$$\LARGE X_{d-proj}=XW_d$$
> $W_d$ is the first d columns of $V$

### Explained Variance Ratio
The pca.explained_variance_ratio_ variable indicates the proportion of the dataset's variance that lies along each principal component. 

### Choosing the number of dimensions
Choose the dimensions that add up to 95% of the variance.
But 2 or 3 for data visualization.

### PCA for compression
Inverse transformations of the data can be applied to revert it back to its original state. The mean squared distance between the original data and reconstructed data is the *reconstruction error*. 

*Equation 8-3. PCA inverse transformation, back to the original number of dimensions*
$$\LARGE X_{recovered}=X_{d-proj}W_d^T$$

### Randomized PCA
Quickly finds an approximation of the first $d$ principal components. It's computational complexity is $O(m\times d^2) +O(d^3)$ instead of $O(m\times n^2)+O(n^3)$. Better when $d$ is much smaller than $n$

### Incremental PCA
The preceding implementations require the whole training set to be in memory. Luckily IPCA algorithms have been developed. They allow the splitting of the data into mini-batches and feed an IPCA one batch at a time. 

previous:
[[Main Approaches for Dimensionality Reduction]]
next:
[[Kernel PCA]]