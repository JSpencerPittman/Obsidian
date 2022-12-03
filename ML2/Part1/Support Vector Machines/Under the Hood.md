# Under the Hood
## Training Objective
**Notation**
> $b$ is the bias term
> $w$ is the weights vector

*Equation 5-2. Linear SVM Classifier Prediction*
$$\LARGE\hat{y}=\left\{\begin{matrix}
0, \text{if }w^Tx+b<0\\ 
1, \text{if }w^Tx+b\geq0
\end{matrix}\right.$$
Decision boundary is where it's equal to 0
The smaller a weight vector the larger the margin. So our goal is to minimize $||w||$ to get the largest margin possible. The margins are often 1 and -1.

In a hard margin system we need the decision function to be greater than 1 for all positive training instances and less than -1 for all negative training instances. 
$$\LARGE t^{(i)}=\left\{\begin{matrix}
1, \text{if }y^{(i)}=1\\ 
-1, \text{if }y=0
\end{matrix}\right.$$
The constraint would be
$$\LARGE t^{(i)}(w^Tx^{(i)}+b)\geq1\text{ (for all instances)}$$
*Equation 5-3. Hard margin linear SVM classifier Objective*
$$\LARGE\begin{align}
&\underset{w,b}{minimize}\frac{1}{2}w^Tw\\
&\text{subject to } t^{(i)}(w^Tx^{(i)}+b)\geq1\text{ for i = 1,2,...,m}
\end{align}$$
Now for soft margin we need to introduce a slack variable $\zeta^{(i)}\geq0$. $\zeta^{(i)}$ measures how much each instance is allowed to violate the margin. 2 conflicting objectives.
1. Minimize $w^Tw$ for largest margins possible
2. Smallest slack variables to reduce marginal violations
The $C$ hyperparameter allows us to define the tradeoff between these two objectives. 

*Equation 5-4. Soft margin linear SVM classifier objective*
$$\LARGE\begin{align}
&\underset{w,b,\zeta}{minimize}\frac{1}{2}w^Tw+C\sum^m_{i=1}\zeta^{(i)}\\
&\text{subject to } t^{(i)}(w^Tx^{(i)}+b)\geq1-\zeta^{(i)}\text{and }\zeta^{(i)}\geq0\text{ for i = 1,2,...,m}
\end{align}$$
## Quadratic Programming
The hard margin and soft margin problems are both convex quadratic optimization problems with linear constraints AKA *Quadratic Programming (QP)* Problems. 

*Equation 5-5. Quadratic Programming Problem*
$$\LARGE\begin{align}
&\underset{p}{Minimze}\hspace{0.25 em}\frac{1}{2}p^THp+f^Tp\\
&\text{subject to }\hspace{0.25 em}Ap\leq b
\end{align}$$
> p ($n_p$ x $1$)
> H ($n_p$ x $n_p$) Identity matrix except $H_{0,0}=0$ for the bias term
> f ($n_p$ x $1$) full of 0s
> A ($n_c$ x $n_p$) Which is practially x but with a bias feature
> b ($n_c$ x $1$) full of -1s

## Dual Problem
Given a constrained optimization problem, known as the *primal problem*, its possible to express a related dual problem. Primal=minimization and Dual=maximization. The solution to the dual problem typically gives a lower bound to the solution of the primal problem. Under some conditions it can be the same as the primal problem. This is the case for the SVM. 

*Equation 5-6. Dual form of the linear SVM objective*
$$\LARGE\underset{\alpha}{minimze}\frac{1}{2}\sum^m_{i=1}\sum^m_{j=1}\alpha^{(i)}\alpha^{(j)}t^{(i)}t^{(j)}x^{(i)^T}x^{(j)}-\sum^m_{i=1}\alpha$$
Subject to $\alpha^{(i)}\geq0$
One you find a $\alpha^{(i)}$ that minimizes equation 5-6 using a QP Solver use equation 5-7 to compute $\hat{w}$ and $\hat{b}$. 

*Equation 5-7. From the dual solution to the primal solution*
$$\LARGE\begin{align}
&\hat{w}=\sum^m_{i=1}\hat{\alpha}^{(i)}t^{(i)}x^{(i)}\\
&\hat{b}=\frac{1}{n_s}\sum^m_{i=1}(t^{(i)}-\hat{w}^Tx^{{(i)}})
\end{align}$$
The dual problem is faster to solve than the primal one when the number of training instances is smaller than the number of features This makes the kernel trick possible.

## Kernelized SVMs
Suppose you want to apply a second-degree polynomial transformation to a two-dimensional training set. The following equation shows the mapping function you want to apply

*Equation 5-8. Second-degree polynomial mapping*
$$\LARGE\phi(X)=\phi(\begin{pmatrix}
x_1\\ 
x_2
\end{pmatrix})=\begin{pmatrix}
x_1^2\\ 
\sqrt{2}x_1x_2\\
x_2^2
\end{pmatrix}$$
Equation 5-9. Kernel trick for a second degree polynomial mapping
$$\LARGE\phi(a)^T\phi(b)=(a^Tb)^2$$
The dot product of the transformed vectors is the square of the dot product of the original vectors. 

If you plug the second degree polynomial into Equation 5-6 you now don't have to transform the vectors at all but plug in the square of their dot product. This saves you from even transforming the set.

A kernel is a function capable of computing the dot product $\phi(a)^T\phi(b)$ based only on the original vectors a and b.

*Equation 5-10. Common Kernels*
$$\LARGE\begin{align}
Linear&: K(a,b) = a^Tb\\
Polynomial&: K(a,b)=(\gamma a^Tb+r)^d\\
Gaussian\hspace{0.1 em}RBF&:K(a,b)=exp(-\gamma||a-b||^2)\\
Sigmoid&: K(a,b)= tanh(\gamma a^Tb+r)
\end{align}$$

*Equation 5-11. Making predictions with a kernelized SVM*
$$\LARGE h_{\hat{w},\hat{b}}(\phi(x^{(n)}))=\sum^m_{i=1}\hat{\alpha^{(i)}}t^{(i)}K(x^{(i)},x^{(n)})+\hat{b}$$
*Equation 5-12. Using the kernel trick to compute the bias term*
$$\LARGE\hat{b}=\frac{1}{n_s}\sum^m_{i=1}(t^{(i)}-\sum^m_{j=1}\hat{\alpha}^{(j)}t^{(j)}K(x^{(i)},x^{(j)}))$$
*Equation 5-13. Linear SVM Classifier Cost Function*
$$\LARGE J(w,b)=\frac{1}{2}w^Tw+C\sum^m_{i=1}max(0,1-t^{(i)}(w^Tx^{(i)}+b)$$
