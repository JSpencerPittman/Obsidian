# Making Predictions
You start at the root node, then child nodes and leaf nodes.
A node's samples attribute counts how many training instances it applies to. A node's value attribute tells you how many training instances of each class this node applies to.  A node's Gini attribute measures its impurity, pure(gini=0) is when all of its are the same class.

*Equation 6-1. Gini Impurity*
$$\LARGE G_i=1-\sum^n_{k=1}p_{i,k}^2$$
> $p_{i,k}$ is the ratio of class $k$ instances among the training instances in the ith node


# Estimating Class Probabilities
A tree can also estimate the probability that an instance belongs to class $k$
First it traverses the tree to find the leaf node of this instance, and then it returns the ration of class k nodes in this node. 

## CART Training Algorithm
This algorithms works by splitting the training set into two subsets using a single feature $k$ and a threshold $t_k$ These are chosen by finding the pair $(k,t_k)$ that produces the purest subsets. 

$$\LARGE
J(k,t_k)=\frac{m_{left}}{m}G_{left}+\frac{m_{right}}{m}G_{right}
$$
> $G_{left/right}$ measures the impurity on the left and right side
> $m_{left/right}$ is the number of instances in the left and right side

Runs recursivley until max_depth is hit. If a split cannot be found to reduce impurity a few other hyperparameters step in as stopping conditions. 

Given that decision trees are usually balanced you usually have a traversal complexity of $O(log_2(m))$ which is independent of the number of features so it scales fairly well with respect to training set size. The training complexity is $O(n\times mlog_2(m))$. 

## Gini Impurity of Entropy
Entropy measures the average information content of a message. 

*Equation 6-3. Entropy*
$$\LARGE H_i=-\sum^m_{i=1}p_{i,k}log_2(p_{i,k})$$
Often the two are equal, however Gini is slightly faster, and gini isolates the most frequent classes in its own branch while entropy makes more balanced trees. 

## Regularization Hyperparameters
Often the trained models will overfit the data often resulting in a nonparametric model because the models parameter number isn't set beforehand. While a parametric model reduces underfitting. 
max_depth is a good approach. 
Min_samples_split is the minimum number of samples a node must have before it can split
Min_samples_leaf is the minimum number of nodes a leaf can have
Min_weight_fraction_leaf is similar to min_samples_leaf but a fraction of the total training instances rather than a 
	specific number
max_leaf_nodes
max_features

Increasing min_ and decreasing max_ will regularize the model

Another approach is an overfitted non parametric model that is then pruned. A node whose children are all leaf nodes is pruned if it's purity improvement is not statisticially significant. 

## Regression
For each node rather than predicting a class predict a value. The values are often the average of the leaf node. 
The CART algorithms works almost the same but now we're trying to reduce the MSE and note the Gini Impurity.

*Equation 6-4. CART cost function for regression*
$$\LARGE\begin{align}
&J(k,t_k) = \frac{m_{left}}{m}MSE_{left}+\frac{m_{right}}{m}MSE_{right}\\
&MSE_{node}=\sum_{i\in node}(\hat{y}_{node}-y^{(i)})^2\\
&\hat{y}_{node} = \frac{1}{m_{node}}\sum_{i\in node}y^{(i)}
\end{align}
$$
## Instability
Decision trees love orthagonal boundaries making them very sensitive to trianing set rotation. Very sensitive to small variations in the training data. 