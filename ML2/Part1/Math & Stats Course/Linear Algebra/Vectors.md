# Vectors
$$\LARGE\vec{r}\cdot\vec{s}=|r||s|cos\theta$$
*Scalar Projection*
$$\LARGE\frac{\vec{r}\cdot\vec{s}}{|r|}=|s|cos\theta$$
*Vector Projection*
$$\LARGE\vec{r}\frac{\vec{r}\cdot\vec{s}}{|r|^2}$$
*Basis is a set of vectors that*
(i) are not linear combinations of each other (linearly indepenedent)
(ii) span the space that is n-dimensional

*Scaling Matrix*
$$\LARGE\begin{bmatrix}
 a& 0\\ 
 0& b
\end{bmatrix}$$
Inverse Matrix
$$\LARGE\begin{align}
&Ar=s\\
&A^{-1}Ar=A^{-1}s\\
&r=A^{-1}s
\end{align}$$
$$\LARGE A^{-1}A=I$$
To find the inverse convert A to the identity matrix and apply same conversions to the identity matrix itself. 
$$\LARGE\frac{1}{ad-bc}\begin{bmatrix}
 d& -b\\ 
 -c& a
\end{bmatrix}=A^{-1}$$
$$\LARGE A^TA=I, A^T=A^{-1}$$
## Eigens
**Eigenvector** remains unchanged in DIRECTION after a transformation, lays in same span 
	before/after transformation
**Eigenvalue** is the scale factor for a eigenvector.

In a scale both the horizontal and vertical vectors are eigenvectors
In a shear transformation only either the horizontal or vertical is an eigenvector
In a rotation there is no eigenvectors

## Special Cases of Eigens
In a uniform scaling any vector is an eigenvector
In a 180 rotation any vector is an eigenvector
In a combination of a vertical scaling and horizontal shear there are two eigenvectors one is 
	the horizontal and the other is in between the diagonal and vertical and vice versa.

## Eigen Basis
A Eigenbasis is a basis where a matrix is diagonal

Applying the same transformation again and again is best done
by converting the transformation matrix to a diagonal matrix apply the sequential transformations and then converting it back into it's original form.