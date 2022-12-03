# Linear Regression
*Equation 4-1. Linear Regression model prediction*
$$\LARGE \hat{y}=\theta_0+\theta_1x_1+\cdots+\theta_nx_n$$
> $\hat{y}$ is the predicted value
> $n$ is the number of features
> $x^i$ is the ith feature value
> $\theta_j$ is the jth model parameter

*Equation 4-2. Linear Regression model prediction (vectorized form)*
$$\LARGE\hat{y}=h_\theta(X)=\theta\cdot X = \theta^TX$$
> $\theta$ model's parameter vector
> $x$ is the instance feature vector

### Measure of how well(or poorly) a model fits the training data
While the RMSE was used it easier in practice and yields the same result to minimize the MSE
*Equation 4-3. MSE cost function for a Linear Regression Model*
$$\LARGE MSE(X,h_\theta)=\frac{1}{m}\sum^m_{i=1}(\theta^Tx^{(i)}-y^{(i)})^2$$

## The Normal Equation
Closed-form approach to minimizing the cost function
*Equation 4-4. Normal Equation*
$$\LARGE\hat{\theta}=(X^TX)^{-1}(X^Ty)$$
> $\hat{\theta}$ is the value of $\theta$ that minimzes the cost function
> $y$ is the vector of target values containing $y^{(1)}$ to $y^{(m)}$

Pros:
	Great with many training sets
	Quick Predictions
	Fast to solve for few features
Cons:
	Scales poorly with many features

## Gradient Descent
The MSE Function is a convex function so there are no local minima to worry about. Also the slope doesn't pander too much staying mostly continous. Make sure all parameters are on the same scale to keep elongated cost functions OUT. 

### Batch Gradient Descent
Trains the WHOLE training set for each iteration

*Equation 4-5. Partial Derivatives of the cost function*
$$\LARGE\frac{\partial}{\partial\theta_j}MSE(\theta)=\frac{2}{m}\sum^m_{i=1}(\theta^Tx^{(i)}-y^{(i)})x_j^{(i)}$$
*Equation 4-6. Gradient vector of the cost function*
$$\LARGE\nabla_\theta MSE(\theta)=\begin{pmatrix}
\frac{\partial}{\partial\theta_0}MSE(\theta)\\ 
\frac{\partial}{\partial\theta_1}MSE(\theta)\\ 
\vdots\\ 
\frac{\partial}{\partial\theta_n}MSE(\theta)
\end{pmatrix}=\frac{2}{m}X^T(X\theta-y)$$
Pros:
	Scales well with many features
Cons:
	Slow on very large training sets

Go opposite of gradient to get downhill(global minima)
*Equation 4-7. Gradient Descent step*
$$\LARGE\theta^{\text{(next step)}}=\theta-\eta\nabla_\theta MSE(\theta)$$
> $\eta$ is the learning rate

To optimize training set a maximum number of iterations and a stop for when the norm of the gradient vector becomes to small or less than $\epsilon$ (tolerance)

### Stochastic Gradient Descent
Unlike Batch Gradient Descent, Stochastic Gradient Descent uses one random training set instead of all of them for each iteration. This allows for only one instance to be required in memory at once as well as faster computation time. 

Because of it's random nature it doesn't decline slowly like batch gradient descent but bounces up and down, decreasing only on average over time. It never quite hits the minimum though like batch gradient descent does. 

Although Stochastic's spontaneousness helps when the cost functions are irregular allowing the function to hop out of local minima. 

A solution to help with SGD's inability to narrow in on a minima is to gradually decrease the learning rate $\eta$ over time. A *learning schedule* determines this rate at each iteration and is a function. 

A iterative round is referred to as an *epoch* which is the amount of times the whole training set is iterated over.

To ensure each instance is selected make sure to shuffle the training set and go through it, iteration by iteration. Then reshuffle per epoch. 

### Mini-Batch Gradient Descent
Compromise of Batch and Stochastic performing gradient descent on random sets of instances for each iteration. This operation gets a performance boost from the hardware optimization of matrix operations using the gpu.

It is however harder for MBGD to escape from a local minima. 

Algorithm | Large m | Out-of-core support | Large N | Hyperparams | Scaling Required | Scikit-Learn
-- | -- | -- | -- | -- | -- | --
Normal Equation | Fast | No | Slow | 0 | No | N/A
SVD | Fast | No | Slow | 0 | No | LinearRegression
Batch GD | Slow | No | Fast | 2 | Yes | SGDRegressor
Stochastic GD | Fast | Yes | Fast | $\geq2$ | Yes | SGDRegressor
Mini-Batch GD | Fast | Yes | Fast | $\geq2$ | Yes | SGDRegressor
