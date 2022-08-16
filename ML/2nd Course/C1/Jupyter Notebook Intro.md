# Jupyter Notebook Intro
**Markdown Cells** cells of text
**Code Cell** full of code

NumPy - Scientific Computing
Matplotlib - Plotting Data
```python
import numpy as np
import matplotlib.pyplot as plt
```

## NumPy
**Arrays**
```python
arr = np.array([v1,v2,...,vn])
# methods
-arr
arr ** power
np.sum(arr)
np.mean(arr)
np.dot(a,b)
# Reshaping
# if a dimension is -1 it's inferred
# if only one integer than a 1-D array of that length is created
arr.reshape(shape)
# Binary operators work element-wise
# of course the vectors must be the saame size
arrA + arrB
# Size as tuple for each dimension
arr.shape
# Type of each data element
arr.dtype
# Array of zeros
np.zeros(shape)
# Evenly spaced values within a given interval
np.arange([start, ]stop, [step, ]dtype=None, *, like=None)
# reshaping
arr.reshape(newShape)
```

## Matplotlib
**Scatter Plot**
```python
# x/y lines
plt.plot(x,y,c='b',label='label of line')
# Here marker is the shape of the point and c is the color
plt.scatter(x,y,marker='x',c='r')
# Title of the graph
plt.title("Title of graph")
# axis labels
plt.ylabel("Label of y-axis")
plt.xlabel("Label of x-axis")
# display legend
plt.legend()
# display graph
plt.show()
# Subplots
plt.subplots(rows, cols, )
```