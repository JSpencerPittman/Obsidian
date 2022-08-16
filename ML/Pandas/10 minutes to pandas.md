### Viewing Data
```python
import pandas as pd

# Top and bottom rows of a frame
df.head()
df.tail()


# display index, columns
df.index
df.columns

# to numpy
df.to_numpy()
## NOTE: df has multiple dtypes: one for each column while numpy has only one for the whole array making it a very expensive operation

# Quick statistic summary of your data
df.describe()

# Transpose
df.T

# Sort by axis
df.sort_index(axis=1, ascending=False)

# sort by values
df.sort_values(by="B")
```

### Data Types
Series: 1D, size-immutable
DataFrame: 2D
Panel: 3D
Index = Rows = Axis 0
Columns = Axis 1

### Pandas Series
`pandas.Series( data, index, dtype, copy)`
Data: Takes various forms like ndarray, list, constants
Index: unique/hashable, same length as data
	The default is np.arange(n) if no index is passed
Dtype: Data Type
Copy: copy data, default is False

Creating a series
```python
# empty
s = pd.Series()

# or
data = np.array(['a','b','c','d'])
s = pd.Series(data)

```

**Accessing Data**
```python
# retrieves the first element
s[0]

# retrieves the first three elements
s[:3]
# the last three
s[-3:]

# using a label (index)
s[['label1','label2','label3']]


```

## DataFrame
`pandas.DataFrame( data, index, columns, dtype, copy)`
Column: for column labels, the optional default syntax is np.arange(n)

**Creating a DataFrame**
```python
# empty
df. pd.DataFrame()

# filled
data = [1,2,3,4,5]
df = pd.DataFrame(data)

data = [['Alex',10],['Bob',12],['Clarke',13]]
df = pd.DataFrame(data, columns=['Name','Age'])
```

**Adding/Deleting Columns**
```python
# Adding a new column
df['new_col']=pd.Series([...],index=[...])

# Deleting a column
del df['col']
df.pop('col')
```

**Row Selection, Addition, Deletion**
```python
# Selection by label
# returns a series
# the name of the series is the label
df.loc['label']

# Selection by integer location
df.iloc[2]

# Selecting multiple rows
df[2:4]

# Adding new rows
df.append(df2)

# deletion of rows
# drops rows with label 0
df.drop(0)
```
