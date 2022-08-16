# Multivariate Gaussian Distrobution
## Parameters
$$x \epsilon \mathbb{R}^n$$
We need to model $p(x)$ as a whole not as separate for each element
$$\begin{align}\mu \epsilon \mathbb{R}^n\\\Sigma\epsilon\mathbb{R}^{nxn}\end{align}$$

The equation for $p(x)$ is as follows
$$
p(x) = \frac{1}{(2\pi)^{\frac{n}{2}}\sqrt{|\Sigma|}}exp(-\frac{1}{2}(x-\mu)^T\Sigma^{-1}(x-\mu))
$$
Here $|\epsilon|$ is representative of the determinant of $\Sigma$

In $\Sigma$ a lower value lowers variance and vice versa along the identity diagonal
Wider | Narrower
-- | --
$\begin{bmatrix}2 & 0\\ 0 & 2\end{bmatrix}$ | $\begin{bmatrix}0.5 & 0\\ 0 & 0.5\end{bmatrix}$
Then with diagonals its the opposite
Wider | Narrower
-- | --
$\begin{bmatrix}1 & 0.5\\ 0.5 & 1\end{bmatrix}$ | $\begin{bmatrix}1 & 0.8\\ 0.8 & 1\end{bmatrix}$

## Algorithm
1) Parameter fitting
$$\begin{align}&\text{Given training set } \{x^{(1)},x^{(2)},\cdots,x^{(m)}\}\\&\mu=\frac{1}{m}\sum^m_{i=1}x^{(i)}\\&\Sigma=\frac{1}{m}\sum^m_{i=1}(x^{(i)}-\mu)(x^{(i)}-\mu)^T\end{align}$$
2) Compute P(x)
3) Flag an anomaly if $p(x) < \epsilon$

## Original vs Multivariate
Original Model | Multivariate Gaussian
-- | ---
Manually create features to capture anomalies where $x_1,x_2$ take unusual combination of values | automatically captures correlations between features
Commputationally Cheaper and scales better to large values of n | computationally more expensive
OK even if there's a small training set | must have $m > n$ or else $\Sigma$ is not invertible
