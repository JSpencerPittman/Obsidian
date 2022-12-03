# Random Forests
An ensemble of decision trees generally trained used the bagging method with max_samples set to the size of the training set. 

### Extra-Trees
To make trees even more random the threshold for features can be selected randomly at each split. This is called an **Extremely Randomized Tree**

### Feature_Importance
Easier to measure relative importance of each feature. Scikit looks at how much node's that use this feature reduce average impurity. Or a weighted average, where each node's weight is equal to the number of training instances assigned to it. Helps with feature selection. 

previous:
[[Random Patches and Random Subspaces]]
next:
[[Boosting]]