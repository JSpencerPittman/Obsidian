## Line Graph
```python
import matplotlib.pyplot as plt

x = [3,1,2]
y = [3,2,1]

plt.plot(x,y)
plt.title("Line Chart")
plt.legend("Line")
plt.show()
```

## Bar Chart
```python
import matplotlib.pyplot as plt

x = [3,1,3,12,2,4,4]
y = [3,2,1,4,5,6,7]

plt.bar(x,y)
plt.title("Bar Chart")
plt.legend("bar")
plt.show()
```

## Histogram
```python
import matplotlib.pyplot as plt

x = [1,2,3,4,5,6,7,4]

plt.hist(x, bins=[1,2,3,4,5,6,7])
plt.title("Histogram")
plt.legend("bar")
plt.show()
```

## Scatter
```python
import matplotlib.pyplot as plt

x = [3,1,3,12,2,4,4]
y = [3,2,1,4,5,6,7]

plt.scatter(x,y)
plt.title("Scatter chart")
plt.legend("A")
plt.show()
```

## Pie Chart
```python
import matplotlib.pyplot as plt

x = [1,2,3,4]
e = (0.1,0,0,0)

plt.pie(x,explode=e)
plt.title("Pie chart")
plt.show()
```

## 3D Plots
```python
import matplotlib.pyplot as plt

x = [1,2,3,4,5]
y = [1,4,9,16,25]
z = [1,8,27,64,125]

fig = plt.figure()
ax = plt.axes(projection = '3d')
ax.plot3D(z,y,x)
```