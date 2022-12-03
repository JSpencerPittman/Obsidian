# Regularized Linear Models
## Ridge Regression/Tikhonov Regularization
Just add this to the cost function
$$\LARGE\alpha\sum^n_{i=1}\theta^2_i$$
This encourages smaller weights. Only use this in training not the cost function of the cross-validation function. 

*Equation 4-8. Ridge Regression Cost Function*
$$\LARGE J(\theta)=MSE(\theta)+\frac{\alpha}{2}\sum^n_{i=1}\theta^2_i$$
Don't regularize the bias term $\theta_0$ however. Utilizes the $\ell_2$ norm. $||w||_2 =$ the $\ell_2$ norm of feature vector $w$.
$$
\LARGE\frac{\alpha}{2}\sum^n_{i=1}\theta^2_i
=\frac{1}{2}(||w||_2)$$

*Equation 4-9. Ridge Regression closed-form solution*
$$\LARGE\hat{\theta}=(X^TX+\alpha A)^{-1}X^Ty$$
## Lasso Regression
**Least Absolute Shrinkage and Selection Operator Regression**
This utilizes the $\ell_1$ norm instead of the $\ell_2$ norm. 

*Equation 4-10. Lasso Regression cost function*
$$\LARGE J(\theta)=MSE(\theta)+\alpha\sum^n_{i=1}|\theta_i|$$
This function tends to set the weights of the least important features to zero.

There are two main differences between ridge and lasso. With ridge as convergence takes place the gradient gradually gets smaller. Second the optimal parameters get closer and closer to the origin when you incrase $\alpha$ but never get eliminated entirely.  Lasso on the other hand needs it $\alpha$ to be decreased for it.

The lasso cost function isn't differentiable for any $\theta_i = 0$ so you need to use a subgradient vector to circumvent this.

*Equation 4-11. Lasso Regression subgradient vector*
$$\LARGE g(\theta,J)=\nabla_\theta MSE(\theta)+\alpha\begin{pmatrix}
sign(\theta_1)\\ 
sign(\theta_2)\\ 
\vdots\\ 
sign(\theta_n)
\end{pmatrix}
$$$$\LARGE\text{ where sign }(\theta_i)=\left\{\begin{matrix}
-1\text{ if }\theta_i<0\\ 
0\text{ if }\theta_i=0\\ 
1\text{ if }\theta_i>0 

\end{matrix}\right.$$
## Elastic Net
Middle Ground of Ridge and Lasso Regression
>$r$ is the mix ratio, 0 = ridge, 1 = lasso

*Equation 4-12. Elastic Net Cost Function*
$$\LARGE J(\theta)=MSE(\theta)+r\alpha\sum^n_{i=1}|\theta_i|+\frac{r-1}{2}\alpha\sum^n_{i=1}\theta^2$$


## How to choose between them?
Assume ridge as a default, but if you suspect only a few features to be useful then use lasso or elastic net as they reduce the useless features down to zero. 

Elastic net is preferred over lasso usually because lasso behaves erratically when the number of features is greater than the number of training instances or when several features are strongly correlated.

## Early Stopping
Stop the training as soon as the validation error reaches a certain minimum. This prevents the model from overfitting. If it's hard to detect the minimum just check when a algorithm has hit a low and if it doesn't get any lower for a period of time then rollback to that minimum. 
[[Code Examples#Early Stopping]]

