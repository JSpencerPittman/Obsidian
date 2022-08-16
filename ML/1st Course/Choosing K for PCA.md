# Choosing K for PCA
First let me define to equations
**Average Squared Projection Error**
$$\frac{1}{m}\sum^m_{i=1}||x^{(i)}-x^{(i)}_{approx}||^2$$
**Total Variation in data**
$$
\frac{1}{m}\sum^m_{i=1}||x^{(i)}||^2
$$
Finally we need to choose a k to be small such that 
$$
\frac{\frac{1}{m}\sum^m_{i=1}||x^{(i)}-x^{(i)}_{approx}||^2}
{\frac{1}{m}\sum^m_{i=1}||x^{(i)}||^2} \leq 0.01
$$
## Algorithms
Try PCA with k = 1
Compute $U_{reduce}$ , $Z$'s, $X_{approx}$'s
Check if
$$
\frac{\frac{1}{m}\sum^m_{i=1}||x^{(i)}-x^{(i)}_{approx}||^2}
{\frac{1}{m}\sum^m_{i=1}||x^{(i)}||^2} \leq 0.01
$$
[U,S,V] = svd(Sigma)
Pick smallest value of k for which
$$
\frac{\sum^k_{i=1}S_{ii}}
{\sum^m_{i=1}S_{ii}}
\geq 0.99
$$
99% of variance retained


