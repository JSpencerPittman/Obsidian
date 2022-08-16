# Gaussian Kernel
Gaussian Equation
$$
\begin{align} 
&e^{-\frac{||x-l^{(i)}||^2}{2\sigma^2}} \\
&e^{-\frac{\sum^n_{j=1}||x_j-l_j^{(i)}||^2}{2\sigma^2}} \\
&K(x,l^{(i)}) = similarity(x,l^{(i)})
\end{align}
$$
Instead of using polynomial features were creating landmarks on a grid like so. 
![[svmLandMarks.png]]
$$
F_i = similarity(x,l^{(i)})
$$
Therefore if x is far from $l^{(i)}$ then $f_i \approx 0$
These landmarks are set as so
$l^{(1)} = x^{(1)}, l^{(2)} = x^{(2)},\cdots,l^{(m)} = x^{(m)}$

The lower $\sigma$ i the narrower it is and vice versa

Cost function using Gaussian kernel is similar to SVM's
$$\begin{align}
&Cost_1(\theta^Tx^{(i)}) = -log(h_\theta(x^{(i)})) \\
&Cost_0(\theta^Tx^{(i)}) = -log(1- h_\theta(x^{(i)})) \\
&\underset{\theta}{min}C\sum^m_{i=1}y^{(i)}Cost_1(\theta^Tf^{(i)}) + (1-y^{(i)})Cost_0(\theta^Tf^{(i)}) + \frac{1}{2}\sum^n_{j=1}\theta^2_j
\end{align}$$

Also fun fact, here's a vectorized version of theta
$$ \frac{1}{2}\sum^n_{j=1}\theta^2_j = \theta^T\theta$$
### Manipulating $C$ and $\sigma$
The higher C is the less bias and more variance there is.
The higher $\sigma$ is the more bias and less variance there is