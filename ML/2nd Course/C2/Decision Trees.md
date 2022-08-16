## Key Decisions to make
1. How do you choose what feature to split on at each node?
	We do this to maximize purity and minimize impurity
2. When do you stop splitting?
	When a node is 100% one class
	When splitting a node will result in the tree exceeding maximum depth
	When improvements in purity score are below a certain threshold
		When number of examples in a node is below a certain threshold
			Return the mode

## Decision Tree Mathematics
V is a random variable with values $v_k$ having probability $P(v_k)$ 
The entropy for this system is defined as
$$\LARGE\begin{align}\text{Entropy: } H(V) &= \sum_kP(v_k)log_2(\frac{1}{P(v_k)})\\&=-\sum_kP(v_k)log_2(P(v_k))\end{align}$$

The entropy of a boolean random variable $B(q)$ is
$$\LARGE B(q) = -(qlog_2(q)+(1-q)log_2(1-q))$$
If a system contains $p$ positive examples and $n$ negative examples then the output of the variable on the whole set is
$$\LARGE H(Output) = B(\frac{p}{p+n})$$
An attribute $A$ with $d$ distinct values divides the training set $E$ into subsets $E_1,\dots,E_d$
Each subset $E_k$ has $p_k$ positve examples and $n_k$ negative examples
Then the remaining information for given attribute $A$ would be
$$\LARGE\text{Remainder}(A)=\sum_{k=1}^d(\frac{p_k+n_k}{p+n})B(\frac{p_k}{p_k+n_k})$$
Information gain would then be 
$$\LARGE\text{Gain}(A)=B(\frac{p}{p+n})-\text{Remainder}(A)$$

## One hot encoding
Great when a feature has more than two categorical values
Turn the feature with multiple features into a seperate one for each value, for example
One attributeHeight- medium, short, tall would become three separate attributes medium, short, tall.

One hot encoding: if a categorical feature can take on $k$ values, create $k$ binary features (0 or 1 valued)

Then recode other attributes with two values as 1's and 0's

This type of encoding also allows data to be fed into a neural network


## Continuous Valued Features
Split data by an inequality

## Regression Tree
Try to reduce variance of the data