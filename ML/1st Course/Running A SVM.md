# Executing a SVM
Use SVM software package to solve for $\theta$
Specify a $C$
Choose a kernel
- None
- Linear
	- y = 1 if $\theta^Tx \geq 0$
	- Use if n = Large and m = small
- Gaussian Kernel
	- Choose $\sigma^2$
	- N = small, m = large

## Kernel Function
function f = kernel($x_1, x_2$)
$f = exp(-\frac{||x_1-x_2||^2}{2\sigma^2})$

#### MAKE SURE TO PERFORM FEATURE SCALING BEFORE GAUSSIAN KERNEL

