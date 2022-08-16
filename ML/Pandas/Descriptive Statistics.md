```python
# Axis = 0 this is the index and we iterate through each row
# If axis = 1 then we iterate through each column
df.sum()
df.sum(1)

df.mean()
df.std()

```

### Other methods
count() - number of non-null observations
median()
mode()
min()
max()
abs()
prod()
cumsum()
cumprod()

describe()
Consider only specific columns
describe(include=['info'])
'all' = summarize all columns
'number' = numeric columns
'object' = string columns
~P.S. also give info() a try~

value_counts()
counts the amount of each value in a column