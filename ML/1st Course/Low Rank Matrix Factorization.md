# Low Rank Matrix Factorization
$$X = \begin{bmatrix}
(x^{(1)})^T\\ 
(x^{(2)})^T\\
\vdots\\ 
(x^{(n_m)})^T\\ 

\end{bmatrix}$$
$$\Theta = \begin{bmatrix}
(\theta^{(1)})^T\\ 
(\theta^{(2)})^T\\
\vdots\\ 
(\theta^{(n_u)})^T\\ 

\end{bmatrix}$$
Predicted Ratings:
$$Y\approx X\Theta^T=\begin{bmatrix}
(\theta^{(1)})^T(x^{(1)}) & (\theta^{(2)})^T(x^{(1)}) & \cdots & (\theta^{(n_u)})^T(x^{(1)}) \\ 
 (\theta^{(1)})^T(x^{(2)})& (\theta^{(2)})^T(x^{(2)}) & \cdots & (\theta^{(n_u)})^T(x^{(2)})\\ 
\vdots & \vdots & \vdots & \vdots \\ 
 (\theta^{(1)})^T(x^{(n_m)})& (\theta^{(2)})^T(x^{(n_m)}) & \cdots & (\theta^{(n_u)})^T(x^{(n_m)})
\end{bmatrix}$$

How to find related objects:
	find the smallest difference 
	$$\text{smallest }||x^{(i)}-x^{(j)}||$$
#### Mean Normalization
Y-$\mu$ returns a array of ratings except the mean of each row is 0
For a user j on movie i predict
	$(\theta^{(j)})^T(x^{(i)}) + \mu_i$
	