# Custom Estimators
```python
# Transformer Mixin - for transformers only
class estimatorName(BaseEstimator, TransformerMixin):
	def __init__(self):
		pass
	def fit(self):
		pass
	def transform(self):
		pass
	def predict(self):
		pass
```

# Pipelines
```python
pipelineName = Pipeline([
	('name', transformer), ...
]])
```
# Column Transformer
```python
pipelineName = ColumnTransformer([
	('name', pipelineName, catNames),...
])
```

