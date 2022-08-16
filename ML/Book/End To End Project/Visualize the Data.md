If a training set is very large you may want to consider an exploration set or copying the training set so as to not modify it just yet.

Map it, color it, expand it, find correlations, be creative there's a link if you look hard enough. 
`df.corr()`

Use scatter matrices for also finding correlations between attributes
```python
from pandas.plotting import scatter_matrix
attributes = ["...","...",...]
scatter_matrix(df[attributes])
```

Try to notice quirks and fix them before training your algorithms

Member this is an iterative process and you can be as thorough as you want, but accept it as a certainty that you'll be back at this stage in no time