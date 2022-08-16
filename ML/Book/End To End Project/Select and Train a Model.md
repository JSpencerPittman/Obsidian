# Select and Train a model
## Training and Evaluating on the Training Set
```python
from sklearn.linear_model import LinearRegression

lin_reg = LinearRegression()
lin_reg.fit(training_set_prepared, training_set_labels)
lin_reg.predict(training_set_prepared)
```

Now look at the error on predictions
```python
from sklearn.metrics import mean_squared_error
train_set_pred = lin_reg.predict(train_set_prep)
lin_mse = mean_squared_error(train_set_prep, train_set_labels)
lin_rmse = np.sqrt(lin_mse)
```

What about decision trees?
```python
from sklearn.tree import DecisionTreeRegressor
tree_reg = DecisionTreeRegressor()
tree_reg.fit(train_set_prep, train_set_labels)
train_pred = tree_reg.predict(train_set_prepared)
```

## Better Evaluation using Cross-Validation
```python
from sklearn.model_selection import cross_val_score
scores = cross_val_score(estimator, train_set_prep, train_set_labels, scoring="neg_mean_squared_error", cv=10)
rmse_scores = np.sqrt(-scores)
```
This is kfolds cross validation by the way
we do negative because a utility function is expected rather than a cost function

The goal isn't to find the best model but get a shortlist of 2-5 ideal models
joblib and pickle are great for storing model's results

