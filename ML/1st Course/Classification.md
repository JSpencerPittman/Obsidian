# Classification
In Binary Classification problems $y \epsilon\{0,1\}$
There's also some Threshold classifier such that
$$\begin{align}
&h(x) > N \hspace{0.25em} then \hspace{0.25em} y = \hspace{0.25em}? \\
&h(x) < N \hspace{0.25em} then \hspace{0.25em} y = \hspace{0.25em}?
\end{align}$$
Except now we are using logistic regression for our hypothesis instead of linear regression. In logistic regression the range of $h_\theta(x)$ is $0 \leq h_\theta(x) \leq 1$.
Heres the equation of logistic regression's hypothesis which revolves around the infamous sigmoid function.
$$\begin{align}
h_\theta(x) &= g(\Theta^TX)\\
g(z) &= \frac{1}{1 + e^{-z}}
\end{align}$$
Below is the infamous sigmoid function that ranges from $0 < y < 1$
![[sigmoidImage.png]]
Y-axis is the probabily that h(x) = 1


#### Decision Boundary
Seperates y = 1 from y = 0

#### Cost Function of Classification
$$
\begin{align}
Cost(h_\theta(x),y) &= \left\{\begin{matrix}
-log(h_\theta(x)), \hspace{0.25em} if \hspace{0.25em}y = 1\\ 
-log(1 - h_\theta(x)), \hspace{0.25em} if \hspace{0.25em}y = 0
\end{matrix}\right.\\
Cost(h_\theta(x),y) &= -ylog(h_\theta(x)) - (1-y)log(1-h_\theta(x))\\
J(\Theta) &= -\frac{1}{m}\sum^m_{i=1}Cost(h_\theta(x^{(i)}),y^{(i)})
\end{align}$$
To understand this you first need to see the image of the $y = -log(x)$ function.

![[-log(x).png]]
Here if y = 1, then the more uncertain it is cost the algorithm more points at an exponential rate and vice versa for the y = 0 case.

while the cost function of linear regression is
$$\begin{align}
Cost(h_\theta(x),y) &= \frac{1}{2}(h_\theta(x) - y)^2\\
J(\Theta) &= \frac{1}{m}\sum^m_{i=1}Cost(h_\theta(x^{(i)}),y^{(i)})
\end{align}$$

#### Vectorized Gradient Descent For Classification
This will be the same as it is for logistic regression except the hypothesis is swapped out with the logistic regression hypothesis


#### What about Multiple Classes
If there are multiple classes such that y can equal multiple discrete values then a
**One VS All** approach will be used. Run a logistic regression for each class and pick the class that the algorithm is most confident about. 