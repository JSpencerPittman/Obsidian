# Fixing Algorithms
## Debugging a learning algorithm
Fixes are as follows
High Variance | High Bias
-------|------
More Training examples | Add polynomial features
Try a smaller set of features | Add more features
Increase $\lambda$ | Decrease $\lambda$

## Machine Learning Diagnostic
Test for what isn't working in a ML Algorithm
Use this as guidance for what will improve its performance
**DO NOT RELY ON YOUR GUT FEELING**
You gut didn't study Machine Learning

## Evaluating a hypothesis
To evaluate a hypothesis set *70%* of the dataset as a training set and the other *30%* as a Test Set.
Learn $\theta$ from the training data and minizing $J(\Theta)$
An error function for Logistic regression would be 
$$err(h_\theta(x),y) = \left\{\begin{matrix}
1, \text{ if } h_\theta(x) \geq 0.5, y=0\\ 
\text{or if } h_\theta(x) \leq 0.5, y=1\\ 
0, \text{ otherwise}\\
\end{matrix}\right.$$
$$ \text{Test Error } = \frac{1}{m_{\text{test}}}\sum^{m_{\text{test}}}_{i=1}err(h_\theta(x^{(i)}_{\text{test}}),y^{(i)}_{\text{test}})$$