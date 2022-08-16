## Grid Search
You can use scikit-learn's GridSearchCV to automate hyperparamter selection and find ideal values

Here I felt it best to not touch original data for sake of understanding
```python
from sklearn.model_selection import GridSearchCV

param_grid = [
    {'n_estimators': [3, 10, 30], 'max_features':[2,4,6,8]},
    {'boostrap':[False], 'n_estimators': [3, 10], 'max_features':[2,3,4]},
]

forest_reg = RandomForestRegressor()

grid_search = GridSearchCV(forest_reg, param_grid, cv=5, scoring="neg_mean_squared_error", return_train_score=True)
grid_search.fit(housing_prepared, housing_labels)
```

Best values stored as two ways
`grid_search.best_params_` or `grid_search.best_estimator_`
 all the cv results are also saved under `grid_search.cv_results_`
 ```python
for mean_score, params in zip(cvres["mean_test_score"], cvres["params"]):
	print(np.sqrt(-mean_score), params)
```

## Randomized Search
Grid Search works for a relativley few combinations, but when the hyperparemeter search space is large, it's often preferable to use `RandomizedSearchCV` instead. 
Random Parameters are selected every iteration. More control over computing budget to allocate to hyperparameter search. 

## Ensemble Methods
Combine the highest performing models, this is an alternative to narrowing down our model to one ideal one.

## Analyze the best models and their errors
Display importance of each attribute to a model with their name
```python
feature_importances = grid_search.best_estimator_.feature_importances_
extra_attribs = ["rooms_per_hhold", "pop_per_hhold","bedrooms_per_room"]
cat_encoder = full_pipeline.named_transformers_["cat"]
cat_one_hot_attribs = list(cat_encoder.categories_[0])
attributes = num_attribs + extra_attribs + cat_one_hot_attribs
sorted(zip(feature_importances, attributes), reverse=True)
```

## Evaluate your system on the test set
Pipeline it, as a transform() NOT fit_transform()
```python
final_model = grid_search.best_estimator_

X_test = strat_test_set.drop("median_house_value", axis=1)
y_test = strat_test_set["median_house_value"].copy()

X_test_prepared = full_pipeline.transform(X_test)

final_predictions = final_model.predict(X_test_prepared)

final_mse = mean_squared_error(y_test, final_predictions)
final_rmse = np.sqrt(final_mse)
```

Want an 95% Confiedence Interval for the generalization error using scipy.stats.t.interval()
```python
from scipy import stats
confidence = 0.95
squared_errors = (final_predictions - y_test)  ** 2
np.sqrt(stats.t.interval(confidence, len(squared_errors)-1,
						loc=squared_errors.mean(),
						scale=stats.sem(squared_errors)))
```