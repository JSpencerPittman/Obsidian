# Bagging and Pasting
How do we diversify classifiers. 
1. Use different training algorithms
2. Use different subsets of training data

**Bagging**
Sampling done with replacement
for same training model
Shorthand for: Bootstrap Aggregating

**Pasting**
Sampling without replacement

**Statistical Mode**
Aggregate function of all the predictors, most often most frequent pick
Otherwise it's average for regression

Each individual model has higher bias than if trained on whole training set. 
Often ensemble has similar bias and lower variance than if single model was trained on whole dataset

These methods often scale well due to it's ability to utilize parallel computing.

### Scikit-Learn
```python
bag_clf = BaggingClassifier(
	DecisionTreeClassifier(), n_estimators=500,
	max_samples=100, bootstrap=True, n_jobs=-1
)
bag_clf.fit(X_train, y_train)
y_pred = bag_clf.predict(X_test)
```

Parameters:
> n_estimators how many seperate classifiers to make
> max_samples is most samples used by individual classifiers
> n_jobs how many cores (-1 if all)

### Out-of-Bag evaluation
**Out-of-Bag instances** are the instances in a bagging method not chosen (oob)

A bagging ensemble can be evaluated using oob instances without the need for a separate validaiton set. 
By setting oob_score=True on scikit-learn this does an automatic oob evaluation. 

previous:
[[Voting Classifiers]]
next:
[[Random Patches and Random Subspaces]]