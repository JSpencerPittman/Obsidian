## Pyplot
Provides functions that interact with the figure, create one, decorate plot, create plotting area within figure

**Figure**
This class is the top-level *container* for all the plots AKA the main window where everything is drawn.

**Axes**
Most basic and flexible components for creating sub-plots. An Axes is an individual plot or graph. 

**Multiple Plots**
```python
# creating a new figure
fig = plt.figure(figsize=(width,height))

# new axes 
ax1 = fig.add_axes([left,bottom,width,height])
ax2 = fig.add_axes([...])

# adding the data to be plotted
ax1.plot([x],[y])
ax2.plot([...],[...])
plt.show()
```

**Multiple Lines - One Plot**
```python
fig = plt.figure(...)
ax = fig.add_axes(...)
ax1 = ax.plot(...)
ax2 = ax.plot(...)
plt.show()
```

**Modifying axis range**
```python
ax.set_xlim(bottom,top)
ax.set_xticklabels(("...","...","...",...))
```

**Subplots**
```python
fig.add_subplot(nrows,ncols,index)
```

**Legend**
```python
plt.legend(["...","..."])
```