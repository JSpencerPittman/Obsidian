## Data Cleaning
Write functions for this so you don't have to redo it for every new dataset
You'll gradually build on this transformation library as you go on

First separate the labels(y) from the rest of the features(x)

Quick Note `df.drop()` doesn't alter the original dataframe but returns a modified one

**How to handle missing values?**
1.Get rid of the corresponding training sets
`training_set.dropna(subset=["column"])`

2.Get rid of the whole atrribute
`training_set.drop("column", axis=1)`

3.Set the values to some value(zero, the mean, the median, ect..)
```python
median/mean/... = ...
training_set["column"].fillna(median/mean/..., inplace=True)
```
The inplace ensures it manipulates the underlying data rather than returning a modified dataframe

Scikit-Learn also provides a handy way of dealing with this problem through **SimpleImputer**. First create a SimpleImputer specifying that you want to replace each attribute's missing values with the median of said attribute
```python
from sklearn.impute import SimpleImputer
imputer = SimpleImputer(strategy="median")
```
although the function can only be called on numerical attributes you need to remove text attributes temporarily. Once this is done you can fit it to the data by doing
```python
imputer.fit(training_set_numerical)
```
Since we calculated the median they will be stored in `imputer.statistics_`
Try to ensure it gets applied to the whole system so as to ensure that new data is also filled. It can be applied like so:
```python
X = imputer.transform(training_set)
```
But this turns it into a numpy array so return it as so
```python
train_set_tr = pd.DataFrame(X, columns=train_set_num.columns, index=train_set_num.index)
```

## Handling Text and Categorical Attributes
To convert categories into integers we can us sklearn's OrdinalEncoder
```python
from sklearn.preprocessing import OrdinalEncoder
ordinal_encoder = OrdinalEncoder()
training_text_encoded = ordinal_encoder.fit_transform(training_text)
```
Categories can be found under
`ordinal_encoder.categories_`

The problem is a lot of ML Algorithms will assume to things are close than others due to their categorically assigned [[Prepare the Data for ML]]number. 
We can use one-hot encoding to handle this practically creating an array with one attribute per categorical value.
```python
from sklearn.preprocessing import OneHotEncoder
encoder = OneHotEncoder()
training_text_1hot = encoder.fit_transform(training_text)
```
We get a sparse matrix so we don't take up much memory storing zero's
If you really want an numpy array just say `sparse_matrix.to_array()`

## Custom Transformers
**Base Classes**
If `TransformerMixin` you get access to `fit_transform()`
If `BaseEstimator` and avoid \*args and \*\*kargs then you get `get_params()` and `set_params()` that are useful for automatic hyperparameter tuning

By the way `np.c_[c1,c2,c3,...]` can stack columns into matrices

Add hyperparameters for any preparation step you may be unsure about

## Feature Scaling
Inputs need to be on similar scales(ranges)
Two approaches are as follows:
**1.*min-max scaling* AKA normalization**
$$\frac{x-min}{max-min}$$
Ranges from 0 to 1

Scikit-learn has a `MinMaxScaler` transformer for this


**2.*Standardization***
$$\frac{x-mean}{deviation}$$
Doesn't have a set range which may be problematic for NNs but is less susceptible to outliers

SciKit-Learn has a `StandardScaler` transformer for this


## Transformation Pipeline
```python
from sklearn.pipeline import Pipeline
from skleanr.preprocessing import StandardScaler

pipeline = Pipeline([
					 ('name', <Class such as StandardScaler>),
					 ...
])

training_set_tr = pipeline.fit_transform(training_set)
```
All but the last estimator must be transformers. The fit() method will call the fit_transform() of all intermediary steps but only fit() on the last one.

This works great for working on all columns at once but what if we need two columns to be handled seperately?
This is where the `ColumnTransformer` comes into play
```python
from sklearn.compose import ColumnTransformer

one_attribs = list(training_set)
two_attribs = [...,...]

full_pipeline = ColumnTransformer([
    ('one', one_pipeline, one_attribs),
    ('two', OneHotEncoder(), two_attribs),
])

training_set_prepared = full_pipeline.fit_transform(training_set)
```

P.S. we get both an dense and sparse matrix so based on nonzero cell ratio it chooses which to return
