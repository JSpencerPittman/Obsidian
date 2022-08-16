# Tensorflow
```python
# Example Code Implementation of a neural network
x = np.array([[200.0, 17.0]])
layer_1 = Dense(units=3, activation='sigmoid')
a1 = layer_1(x)

layer_2 = Dense(units=1, activation='sigmoid')
a1 = layer_2(a1)
```

In tensorflow we can't use np.array without making our input a matrix with one row and and a column for each feature, can't be a 1-D Vector Example = (1, n) not (n, )

```python
x = np.array([[200.0,17.0]])
layer_1 = Dense(units=3, activation='sigmoid')
a1 = layer_1(x)
# Here a1 is represented as so
tf.Tensor([[0.2,0.7,0.3]], shape=(1,3), dtype=float32)
# convert a Tensor into a numpy array
a1.numpy()
# represented as
np.array([[1.4661001,1.125196,3.2159438]], dtype=float32)
```

In tensorflow, all matrices are represented as Tensors.

### Building a neural network architecture
```python
layer_1 = Dense(units=3,activation='sigmoid')
layer_2 = Dense(units=1,activation='sigmoid')

model = Sequential([layer_1, layer_2])
#or
model = Sequential([
					Dense(units=3,activation='sigmoid'), 
					Dense(units=1,activation='sigmoid')
				])

model.compile(...)
model.fit(x,y)

model.predict(x_new)
```
### Specifying Input
tf.keras.Input specifies the dimension of the first layer/input layer
```python
model = Sequential(
	[
		tf.keras.Input(shape=(400,)),
		## Layers here ##			   
	], name="my_model"
)
```
### Analyzing layers
```python
# Get layers
modelName.layers
# find weights
weights, bias = layerName.get_weights()
```
## Training NN
We need to train our neural network
```python
from tensorflow.keras.losses import BinaryCrossentropy
# Setup the neural network with a loss function
model.compile(loss=BinaryCrossentropy())
# Epochs is how many iterations of GD we wish to run
# minimizes cost of the nn
model.fit(X,Y,epochs=100)
```

## Overarching steps
1. Create the model
2. Loss and cost functions
	- The logistic regression loss function is called binary cross entropy
	- MeanSquaredError loss function can be used for regression problems
3.  Gradient Descent

## New Activation Functions
```python
model = Sequential([
	Dense(units = 25, activation='relu'   ),
	Dense(units = 15, activation='relu'   ),
	Dense(units =  1, activation='sigmoid')					
])

```

## Summary?
```python
model.summary()
history = model.fit(...)
```

## Imports
tensorflow
tensorflow.keras - Sequential
tensorflow.keras.layers - Dense
tensorflow.keras.losses - BinaryCrossentropy
tensorflow.keras.losses - MeanSquaredError