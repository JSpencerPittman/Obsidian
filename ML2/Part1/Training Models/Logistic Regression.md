# Logistic Regression
Estimate the probability that an instance belongs to a certain class.

*Equation 4-13. Logistic Regression model estimated probability (vectorized form)*
$$\LARGE \hat{p} = h_\theta(x)=\sigma(\theta^Tx)$$
> $\sigma$ is representative of the sigmoid function tha outputs a number between 0 and 1

*Equation 4-14. Logistic Regression*
$$\LARGE\sigma(t)=\frac{1}{1+e^{-t}}$$
*Equation 4-15. Logistic Regression model prediction*
$$\LARGE\hat{y}=\left\{\begin{matrix}
0 \text{ if }\hat{p} < 0.5\\ 
1 \text{ if }\hat{p} \geq 0.5
\end{matrix}\right.$$

*Equation 4-16. Cost function of a single training instance*
$$\LARGE c(\theta) = \left\{\begin{matrix}
-log(\hat{p})\text{ if } y=1\\ 
-log(1-\hat{p})\text{ if } y=0
\end{matrix}\right.$$

*Equation 4-17. Logistic Regression cost function (log loss)*
$$\LARGE J(\theta) = -\frac{1}{m}\sum^m_{i=1}[y^{(i)}log(\hat{p}^{(i){}})+(1-y^{(i)})log(1-\hat{p}^{(i)})]$$
This equation is convex. 

*Equation 4-18. Logistic cost function partial derivatives*
$$\LARGE\frac{\partial}{\partial\theta_j}J(\theta) = \frac{1}{m}\sum^m_{i=1}(\sigma(\theta^Tx^{(i)})-y^{(i)})x_j^{(i)}$$
Decision boundary is where the function is at 50% probability. 

## Softmax Regression
Logistic Regression generalized to support multiple classes directly. Given an $x$ it calculates a score for each class $k$ then estimates the probability of each class by applying the softmax function (*normalized eponential*) to the scores. 
$$\LARGE s_k(x)=(\theta^{(k)})^Tx$$
> $\theta^{(k)}$ each class contains its own parameters
> $\Theta$ each row is a $\theta^{(k)}$

*Equation 4-20. Softmax function*
$$\LARGE \hat{p}_k=\sigma(s(x))_k=\frac{e^{s_k(x)}}{\sum^K_{j=1}e^{s_j(x)}}$$
> $K$ is the number of classes
> $s(x)$ is the vector containing the scores of each class for instance $x$
> $\sigma(s(x))_k$ is the estimated probability that the instance $x$ belongs to class $k$

*Equation 4-21. Softmax Regression classifier prediction*
$$\LARGE\hat{y}=\underset{k}{argmax}\hspace{0.1 em}s_k(x)=\underset{k}{argmax}((\theta^{(k)})^Tx)$$
Cross-entropy penalizes a model when it estimates a low probability for a target class.
*Equation 4-22. Cross entropy cost function*
$$\LARGE J(\theta)=-\frac{1}{m}\sum^m_{i=1}\sum^K_{k=1}y_k^{(i)}log(\hat{p}_k^{(i)})$$
*Equation 4-23. Cross Entropy graident vector for class k*
$$\LARGE\nabla_{\theta^{(k)}}J(\Theta)=\frac{1}{m}\sum^m_{i=1}(\hat{p}^{(i)}_k-y^{(i)}_k)x^{(i)}$$
Compute this for every class and find the parameter matrix $\Theta$ that minimizes the cost function. 