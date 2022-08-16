# Cost Functions
## Squared Error Function
$$\underset{\theta_{0},\theta_{1}}{minimize} \hspace{0.25 em}\frac{1}{2m}\sum_{i = 1}^{m}(h_{\theta}(x^{(i)})-y^{(i)})^{2} = J(\theta_{0},\theta_{1})$$
## Gradient Descent Algorithm
Repeat Until Convergence {
	$\theta_{j} := \theta_{j} - \alpha\frac{\partial }{\partial \theta_{j}}J(\theta_{0},\theta_{1})$ 
}, {
$temp_{0} := \theta_{0} - \alpha\frac{\partial }{\partial \theta_{j}}J(\theta_{0},\theta_{1})$
$temp_{1} := \theta_{1} - \alpha\frac{\partial }{\partial \theta_{j}}J(\theta_{0},\theta_{1})$
$\theta_{0} := temp_{0}$
$\theta_{1} := temp_{1}$
}

This allows each theta to be updated simultaneously and not affect one or the other
>[!What is the alpha symbol?]
>The $\alpha$ is the learning rate
>If this is too high the learning algorithm may skip over the solution
>If it's too low it may take too long to reach an optimal solution

$$\frac{\partial}{\partial \theta_{0}}J(\theta_{0},\theta_{1}) = \frac{1}{m}\sum_{i=1}^{m}(h(x^{(i)})-y^{(i)})$$$$
\frac{\partial}{\partial \theta_{1}}J(\theta_{0},\theta_{1}) = \frac{1}{m}\sum_{i=1}^{m}(h(x^{(i)})-y^{(i)})x^{(i)}$$


#### When do we declare Convergence?
Declare Convergence if $J(\Theta)$ decreases by less than a small value ε after each iteration.

#### Polynomial Regression
This is when we incorporate exponents and alternative types of functions into our hypothesis such as what follows
$$h_\theta(X) = \theta_o + \theta_1x_1 + \theta_2x_2 + \theta_3x_1^2+\theta_4x_2^2$$
### Normal Equation
**Do not feature scale for this!!!**
A method to solve for theta analytically rather than iterativley like gradient descent
$$\Theta = (X^TX)^{-1}X^TY$$
Gradient Descent | Normal Equation
------------ | ------------ 
Have to choose an $\alpha$ | Don't choose an $\alpha$
Many Iterations| No Iterations
Works well even with large n-features | need to compute $(X^TX)^{-1}$ which is nxn
Takes $O(kn^2)$ time | Takes $O(n^3) time$
