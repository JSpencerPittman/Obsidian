## Frame the problem
You need to look at the big picture. Is there a pipeline?
Whats the purpose? Whats happening with your output. 

What does the current solution look like?

Supervised, Unsupervised, Reinforcment?
Classification, Regression, else?
Batch, Online?

## Select a performance Measure
**Root mean square error**
$$
\text{RMSE}(X, h)=\sqrt{\frac{1}{m}\sum^m_{i=1}(h(x^{(i)})-y^{(i)})^2}$$
This function carriers a higher weight for larger errors

**Mean absolute error**
$$\text{MAE}(X, h)=\frac{1}{m}\sum^m_{i=1}|h(x^{(i)})-y^{(i)}|$$
This is a great cost function if there are many errors expected

Both are ways of calculating distance between the prediction and target value vectors

RMSE results in the Euclidean norm, or the notion of distance, $l_2$, $||\cdot||_2$

MAE results in the $l_1$ norm noted $||\cdot||_1$, Manhattan norm, measures the distance between two points using only orthagonal directions

The $l_k$ norm is $||v||_k =(|v_0|^k+|v_1|^k+\dots+|v_n|^k)^{1/k}$
The higher k is the more it focuses on larger numbers and neglects small ones. Hence RMSE being very sensitive to outliers. 

