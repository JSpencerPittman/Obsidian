# Multivariate Linear Regression
$x_{i}$ = feature
*n* = # of features
### Hypothesis
$$h_{\theta}(x)  = \theta_{0} + \theta_1x_1 + \theta_2x_2 + \cdots + \theta_nx_n$$
This is based on the fact that $x_0 = 1$ and the matrices are as follows
$$X = \begin{bmatrix}x_0
\\ x_1
\\ \vdots 
\\ x_n

\end{bmatrix}
\hspace{3 em}
\Theta = \begin{bmatrix}\theta_0
\\ \theta_1
\\ \vdots 
\\ \theta_n

\end{bmatrix}$$
### Cost Function
This is the new Gradient Descent algorithm for multiple variables
$$\theta_j := \theta_j - \alpha\frac{\partial}{\partial\theta_j}J(\Theta)$$
$$\frac{\partial}{\partial \theta_j}J(\Theta) = \frac{1}{m}\sum_{i=1}^{m}(h(x^{(i)})-y^{(i)})x^{(i)}_j$$
### Vectorized Gradient Descent
$$\Theta := \Theta - \alpha\delta$$$$
\begin{align}
\delta &= \frac{1}{m}\sum^m_{i=0}(h_\theta(x^{(i)})-y^{(i)})x^{(i)}= X\Theta - y \\
Z &= \frac{\alpha}{m}sum([\delta.*X],1)
\end{align}
$$
$$
\begin{align}
Temp &= \Theta - [\frac{\alpha}{m}sum([(X\Theta-y).*X],1)] \\
&= \Theta - [\frac{\alpha}{m}sum([\delta.*X],1)] \\
&= \Theta - Z^T
\end{align}
$$
$$\begin{align}
J(\Theta) &= \frac{\delta^T\delta}{2m} \\
&= (2m)^{-1}sum(\delta^2)
\end{align}$$
