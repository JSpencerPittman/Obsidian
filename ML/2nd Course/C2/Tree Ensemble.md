## Tree Ensemble
It's too sensitve to new data
One training example can create a completley different tree
	Making the algorithm not very robust

A tree ensemble is a collection of decision trees
For a prediction the trees vote on their prediction

## Sampling with replacement
Randomly choose a sample and put it back into the selection pool
The selection in one iteration should be independent of past selections

## Sampling with Replacment and Ensemble?
Sample with replacment multiple times and train multiple decision trees on these separate examples

## Random Forest Algorithm
Given a training set of size $m$
For $b =1 \text{ to } B:$
	Use sampling with replacement to create a new training set of size $m$
	Train a decision tree on the new dataset
Ideal B: 64<->128

To further randomize the feature choice
	At each node, when choosing a feature to use to split, if $n$ features are available, pick a random subset of $k < n$ features and allow the algorithm to only choose from that subset of features
This allows the trees to be even more diverse than each other, but should only be used in larger problems.

## Boosted Trees
This algorithm is very similar to the random forest algorithm however instead of picking from all examples with equal $\frac{1}{m}$ probability, make it more likely to pick examples that the previously trained trees misclassify.

## XGBoost - eXtreme Gradient Boosting
Open source implementation of boosted trees
Fast efficent implementation
good choice of default splitting criteria and criteria for when to stop splitting
built in regularization to prevent overfitting
highly competitive algorithm for ML Competitions

Classification
```python
from xgboost import XGBClassifier

model = XGBClassifier()
model.fit(X_Train, y_train)
y_pred = model.predict(X_test)
```

Regression
```python
from xgboost import XGBRegressor

model = XGBRegressor()
model.fit(X_train,y_train)
y_pred = model.predict(X_test)
```

## Decision and Tree Ensembles VS Neu. Net.
**Decision Trees**
	Works well on tabular (structured) data
	Not recommended for unstructured data (images, audio, text)
	Fast
	Small decision trees may be human interpretable

**Neural Networks**
	Works well on all types of data, including tabular and unstructured data
	May be slower than a decision tree
	Works with transfer learning
	When building a system of multiple models working together, it might be easier to string 
		together multiple neural networks
		