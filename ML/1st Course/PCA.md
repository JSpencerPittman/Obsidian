# Principal Component Analysis
## PCA Algorithm
Data Preprocessing
	Training Set: $x^{(1)}, x^{(2)}, \cdots, x^{(m)}$
	Preprocessing: Feature Scaling, mean normalization
		$\mu_j = \frac{1}{m}\sum^m_{i=1}x^{(i)}_j$
		replace each $x^{(i)}_j$ with $x_j - \mu_j$
		if there are different feautures on different scales, scale the features to have a comparable range of values.
PCA
	Reduce data from n -> k dimensions
	compute the covariance matrix
		$$\Sigma = \frac{1}{m}\sum^n_{i=1}(x^{(i)})(x^{(i)})^T$$
		Compute the eigenvectors of matrix $\Sigma$
		```[U,S,V] = svd(Sigma)```
		$$U = \begin{bmatrix}
 \vdots&  \vdots&\vdots&\vdots \\ 
 \mu^{(1)}&  \mu^{(2)}& \vdots &\mu^{(n)} \\ 
 \vdots& \vdots & \vdots & \vdots
\end{bmatrix}$$ In this matrix the eigenvectors are the first k columns.
```
	uReduce = U(:, 1:k)
	z = uReduce'*x
```

To uncompress X from this we can do
$X = U_{\text{reduce}}Z$


## When to use PCA
Use PCA as a NEED not a WANT
It reduces memory required and speeds up a learning algorithm.
Don't use to stop overfitting. 
		