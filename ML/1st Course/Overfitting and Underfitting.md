# Over/Under Fitting
## Underfitting
If an algorithm doesn't fit the training set it may be suffering from high bias and be too restricted to properly fit.
"Strong perception that the data fits a certain way"

## Overfitting
Algorithm only fits the training data and adapts terribly to the test/cv datasets. This is signs of too much variance, the algorithm has too much wiggle room after fitting the training set. 

To fix overfitting we can reduce features through either model selection or manually
Another way is through regularization where we reduce the magnitudes of thetas. Smaller $\theta$'s make algorithms less prone to overfitting. 

## Regularization
To regularize we use the regularization parameter $\lambda$. The equation we use is
$$\frac{1}{2m}\sum^{m}_{i=1}(h_\theta(x^{(i)}) - y^{(i)})^2 + \lambda\sum^n_{j=1}\theta_j^2$$
Here the left side fits the training set while the right-hand side minimizes the $\theta$s.
The derivative of the $\theta_j$ with regularization. 
$$\frac{\partial J(\Theta)}{\partial\theta_j} := \frac{1}{m}\sum^m_{i = 1}(h_\theta(x^{(i)})-y^{(i)})x^{(i)}_j + \frac{\lambda}{m}\Theta$$
Regularized Gradient Descent(Also for the normal equation)
 $$
 \begin{align}
 \theta_j &= \theta_j(1-\frac{\alpha}{m}\lambda) - \sum^m_{i = 1}(h_\theta(x^{(i)})- y^{(i)})x_j^{(i)} \\
 \Theta &= (X^TX + \lambda[])^{-1}X^Ty
 \end{align}
 $$
 Regularized Logistic Regression
 $$J(\Theta) = -\frac{1}{m}(ylog(h_\theta(x^{(i)}))+(1-y)log(1-h_\theta(x^{(i)})) + \frac{\lambda}{2m}\sum^n_{j=1}\theta^2_j$$
 