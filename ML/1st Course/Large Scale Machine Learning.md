# Large Scale Machine Learning
"It's not the best algorithm but who has the most data that wins"
Check if you actually need that much data
	If on a smaller dataset you notice high variance then avail yourself with more data.

### Stochastic Gradient Descent
It's too expensive to run through each training set for every iteration
Here we compare the Batch Gradient Descent to Stochastic Gradient Descent

**Batch Gradient Descent**
m examples per iteration
$$\begin{align}&J_{train}(\theta) = \frac{1}{2m}\sum^m_{i=1}(h_\theta(x^{(i)})-y^{(i)})^2\\
&\text{repeat \{}\\
&\text{ }\theta_j:=\theta)j-\alpha\frac{1}{m}\sum^m_{i=1}(h_\theta(x^{(i)})-y^{(i)})x_j^{(i)}\\
&\text{ (for every }j=0,\dots,n\text{)}\\
&\text{\}}
\end{align}$$
**Stochastic Gradient Descent**
1  example per iteration
1. Randomly shuffle the dataset
2. Repeat {
	for $i=1,\dots,m$ {
		$\theta_j:=\theta_j-\alpha(h_\theta(x^{(i)})-y^{(i)})x_j^{(i)}$
			for $j=0,\dots,n$
		}
	}
This goes through each training example once

**Mini-Batch Gradient Descent**
b examples per iteration
Chosen training examples like so
	$(x^{(i)},y^{(i)}),\dots,(x^{(i+[b-1])},y^{(i+[b-1])})$
This is like batch gradient descent but fewer examples at any given time

## Checking for convergence
How to make sure your algorithms converging with stochastic gradient descent
	For every 1000 iterations plot the averaged cost
	A smaller learning rate can return better values
	If there's too much noise perhaps increase the amount of iterations per 
		plot point
	If the algorithm is diverging use a smaller $\alpha$


We can also decrementally decrease $\alpha$ overtime
	$\alpha = \frac{b}{iteration + c}$
	although now you have two new constants to work with
	
# Online Learning
The problem with online learning is you get continous flow of input data

Repeat forever {
	Get (x,y) corresponding to user
	update $\theta$ using just this example similar to stochastic gradient descent
	$\theta_j:=\theta_j-\alpha(h_\theta(x^{(i)})-y^{(i)})x_j^{(i)}$
			for $j=0,\dots,n$
	Discard example
}
These can adapt to changing user preferences

# Map reduce and Data Parallelism
Split training sets up for multiple machines. Then find the aggregate of all four generated $\theta$'s and this will culminate in the solution.

Great if algorithm can be explained as a summation over the training set