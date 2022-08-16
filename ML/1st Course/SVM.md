# Support Vector Machine
SVM Takes an alternative view of logistic regression, rather than using the hypothesis
$$h_\theta(x) = \frac{1}{1 + e^{-\theta^Tx}}$$
to get some value in **between** 0 and 1 SVM prefers the value to be
$$
\begin{align}
y &= 1, \text{ then } h_\theta(x) \approx 1, \hspace{0.5 em} \theta^Tx >> 0 \\
y &= 0, \text{ then } h_\theta(x) \approx 0, \hspace{0.5 em} \theta^Tx << 0
\end{align}
$$
The cost function for this is similar but now it's a piecewise function of linear components as what follows
![[svm cost.png]]

Then there's the SVM Margin
![[svmMargin.png]]
Here the larger the margin the more it's supported by SVM

The cost function for SVM is
$$\begin{align}
&Cost_1(\theta^Tx^{(i)}) = -log(h_\theta(x^{(i)})) \\
&Cost_0(\theta^Tx^{(i)}) = -log(1- h_\theta(x^{(i)})) \\
&\underset{\theta}{min}C\sum^m_{i=1}y^{(i)}Cost_1(\theta^Tx^{(i)}) + (1-y^{(i)})Cost_0(\theta^Tx^{(i)}) + \frac{1}{2}\sum^n_{j=1}\theta^2_j
\end{align}$$
 Here C is the inverse ($\lambda^{-1}$ ) of $\lambda$.

## Decision Boundary
$z = \theta^Tx^{(i)}$
Whenever $y^{(i)} = 1$ then $z \geq 1$
Whenever $y^{(i)} = 0$ then $z \leq -1$

 