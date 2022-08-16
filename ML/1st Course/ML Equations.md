
## Substitutions
$$
\begin{align}
k &= \frac{1}{m}\\
\delta &= h(x) - y\hspace{1 em} Context-Dependent\\
R &= \frac{\lambda}{2}\sum^n_{j = 1}\theta_j^2\\
R_d &= \lambda\theta_j
\end{align}
$$

## Linear Regression
#### Hypothesis
$$h_\theta(x) = \Theta^TX$$
#### Cost Function
$$
\begin{align}
J(\Theta) &= k\sum^m_{i = 1}\delta^2\\
Cost(x,y) &= (x-y)^2\\
J(\Theta) &= \frac{k}{2}\sum^m_{i = 1}Cost(x^{(i)},y^{(i)})
\end{align}
$$
#### Regularized Cost Functions (Not $\theta_0$)
$$
Regularized(J(\Theta)) = J(\Theta) + kR
$$
## Logistic Regression
Hypothesis, except the $h_{linear}(x)$ in the denominator is the linear hypothesis
$$h_\theta(x) = \frac{1}{1 + e^{-h_{linear}(x)}}$$
#### Cost Function
$$
\begin{align}
J(\Theta) &= -k\sum^m_{i = 1}y^{(i)}log(h_\theta(x^{(i)}))+(1-y^{(i)})log(1-h_\theta(x^{(i)}))\\
Cost(x,y) &= -ylog(h_\theta(x))-(1-y)log(1-h_\theta(x))\\
J(\Theta) &= \frac{k}{2}\sum^m_{i = 1}Cost(x^{(i)},y^{(i)})
\end{align}
$$
#### Regularized Cost Functions (Not $\theta_0$)
$$
Regularized(J(\Theta)) = J(\Theta) + kR
$$
## Gradient Descent
These equations are the same for both linear and logistic regression
#### Unregularized
$$G = \alpha k\sum^m_{i = 1}\delta x^{(i)}_j$$
#### Regularized
$$\begin{align} 
Regularized(G) &= \theta_j - \alpha k[\sum^m_{i=1}\delta x_j^{(i)} + R_d]\\
&= \theta_j(1 - \alpha\lambda k) - \alpha k\sum^m_{i=1}\delta x_j^{(i)}
\end{align}$$
