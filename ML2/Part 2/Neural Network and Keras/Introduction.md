# ANN's and Keras
ANNS often outperform normal models on large complex problems.

## The Perceptron
An ANN architecture, one of the simplest at that, based on a artifical neuron called a threshold logic unit (TLU). Or linear threshold unit. Inputs and outputs are numbers and each connection has an associated weight. The TLU computes the weighted sum as $z = w_1x_1+w_nx_n=x^Tw$ then applies a step function to that sum and outputs
$h_w(x)=step(z)$ 

A common step function used in perceptrons is the Heaviside step function or sign function.
*Equation 10-1. Common step functions used in perceptrons (assuming threshold = 0)*
$$\LARGE heaviside(z)=\left\{\begin{matrix}
0 \text{ if }z<0\\ 
1 \text{ if }z\geq0
\end{matrix}\right.$$
$$\LARGE sgn(z)=\left\{\begin{matrix}
-1 &\text{ if z < 0}\\ 
0 &\text{ if z = 0}\\ 
+1 &\text{ if z > 0}
\end{matrix}\right.$$

**Dense Layer/Fully connected layer**
Every neuron connected to every neuron in previous layer

Usually a bias feature us added as $x_0=1$ 

*Equation 10-2. Computing the outputs of a fully connected layer*
$$\LARGE h_{w,b}(X)=\phi(XW+b)$$
> $X$ is a m x n matrix
> $W$ excluding the bias neuron its an (# of input neurons) x (# neuron in layer)
> $b$ is an (# neuron in layer) x 1
> $\phi$ is an activation function (with TLU's its a step function)

Hebbian Learning
Cells that fire together wire together

*Equation 10-3. Perceptron learning rule (weight update)*
$$\LARGE w_{i,j}^{\text{(next step)}}=w_{i,j}+\eta(y_j-\hat y_j)x_i$$
> $w_{i,j}$ connection weight between the ith input and jth output neuron
> $x_i$ is the ith input value for the current training instance
> $\hat y_j$ is the predicted of the jth output neuron
> $y_j$ is the target output of the jth output neuron
> $\eta$ is the learning rate

*Perceptron Converegence Theorem*
If two points are linearly separable the algorithm will converge to a solution

**Multilayer Perceptron and Backpropgation**
One passthrough input layer, one or more layers of TLUs called hidden layers and one final layer called the output layer
Lower is closer to input, upper is closer to output. Only the output layer posseses no bias neuron. 

**Feedforward neural network**
Flow is from front to back

The backpropogation training algorithm made training NN's possible. It's practically gradient descent using an efficent technique for computing the gradients automatically. 

In just one sweep back to front and to back again it can compute the networks error with regard to every single model parameter. How much each weight and bias term should be tweaked. One it has these gradients it just performs a regular gradient descent step and the whole process is repeated until the network converges to a solution. 

Automatically computing gradients is called automatic differentiation or autodiff. 

Backprop makes a prediction and measures the error then goes through each layer in reverse to measure the error contribution from each connection. Tweaks to reduce error. Forward pass -> Reverse pass -> Gradient Descent

Don't initialize each neuron with the same parameters.

This backprop function doesn't work with the normal step function but it does with a sigmoid function. Step has only flat surfaces which can't have gradient descent calculated on them. Sigmoid is a nonzero slope function.
Some other alternatives are

*hyperbolic tangent function*
$tanh(z)=2\sigma(2z)-1$
-1 to 1 unlike sigmoids 0 to 1
data centered around 0 making convergence faster

Rectified Linear Unit (RELU)
$ReLU(z)=max(0,z)$
Continous but not differentiable at z = 0
No max value helps out

Don't use activation function in final layer

consider softplus
$softplus(z)=log(1+exp(z))$
Close to 0 when z is negative and close to z when z is positive

Loss is typically mean squared error but with many outliers you may prefere mean absolute error or huber
Huber is quadratic when the error is smaller than a threshold (typically 1) but linear when the error is larger than this threshold reducing sensitivity to outliers. 

### Typical Regression MLP Architecture
No. of input neurons, one per feature
No. of hidden layers, depends on problem but typically 1-5
No. of neurons per layer, depends on problem but typically 10-100
No. of output neurons, 1 per prediction dimension
Hidden Activation Relu(or Selu)
Output Activation None, or Relu/softplus(if positive) or logistic/tanh(if bounded)
Loss function: MSE or MAE/Hubers(if outliers)

### Typical Classification MLP Architecture
Hyperparameter | Binary | Multilabel Binary | Multiclass
-- | -- | -- | --
Input and hidden layers | Same as regression | Same as regression | Same as regression
No. of output neurons | 1 | 1 per label | 1 per class
Output layer activation  | Logistic | Logistic | Softmax
Loss Function | Cross entropy | Cross entropy | Cross entropy

## Sequential MLP Example
```python
## PREPROCESSING
import tensorflow as tf
from tensorflow import keras
fashion_mnist = keras.datasets.fashion_mnist
(X_train_full, y_train_full), (X_test, y_test) = fashion_mnist.load_data()
X_valid, X_train = X_train_full[:5000] / 255.0, X_train_full[50000:] / 255.0
y_valid, y_train = y_train_full[:5000], y_train_full[50000:]
X_test = X_test / 255.0
## END OF PREPROCESSING

model = karas.Sequential([
    keras.layers.Flatten(input_shape=[28,28]),
    keras.layers.Dense(300, activation='relu'),
    keras.layers.Dense(100, activation='relu'),
    keras.layers.Dense(10, activation='softmax')
])
```

View a summary with `model.summary()`
And the layers at `model.layers` and the name at `model.layers[i].name`
Weights found at `model.layers.[i].get/set_weights()`

### Compiling the model
No we call the compile method to provide a loss function and optimizer
```python
model.compile(loss="sparse_categorical_crossentropy",
              optimizer="sgd",
              metrics=["accuracy"]
)
```
Here "sparse_categorical_crossentropy" is equivalent to:
	keras.losses.sparse_categorical_crossentropy
Also "sgd" is equivalent to:
	keras.optimizers.SGD()
and "accuracy" is equivalent to:
	keras.metrics.spare_categorical_accuracy

With binary or binary multilabel classification we'd do sigmoid for activation and binary_crossentropy loss

The optimizer is what we will train the model with. 

### Training and Evaluating a model
```python
history = model.fit(X_train, y_train, epochs=30, validation_data=(X_valid, y_valid))
```
For validation_data you can also use validation_split
If some classes are inbalanced perhaps use the class_weight parameter which gives a larger weight to underrepresented classes. You can also mess with per sample weights.

fit() returns a history object containing the training params and list of epochs and the loss and extra metrics

The training error is calculated during an epoch and should be shifted by half an epoch to the left

Optimizing
Learning rate,
optimizer

Generalization is calculated with model.evaluate

### Functional API
Here we plug the input layer into the beginning and once more into the concatenate layer
```python
input_ = keras.layers.Input(shape=X_train.shape[1:])
hidden1 = keras.layers.Dense(30, activation='relu')(input_)
hidden2 = keras.layers.Dense(30, activation='relu')(hidden1)
concat = keras.layers.Concatenate()([input_, hidden2])
output = keras.layers.Dense(1)(concat)
model = keras.Model(inputs=[intput_], outputs=[output])
```

Here we have a wide and deep input. Deep goes through a whole neural network while wide skips over and joins in at the end.
```python
input_A = keras.layers.Input(shape=[5], name="wide_input")
input_B = keras.layers.Input(shape=[6], name="deep_input")
hidden1 = keras.layers.Dense(30, activation='relu')(input_A)
hidden2 = keras.layers.Dense(30, activation='relu')(hidden1)
concat = keras.layers.Concatenate([input_A, hidden2])
output = keras.layers.Dense(1, name="output")(concat)
model = keras.Model(inputs=[input_A, input_B], outputs=[output])
```

Here we have an auxillary output for the deep learning path. 
```python
input_A = keras.layers.Input(shape=[5], name="wide_input")
input_B = keras.layers.Input(shape=[6], name="deep_input")
hidden1 = keras.layers.Dense(30, activation='relu')(input_A)
hidden2 = keras.layers.Dense(30, activation='relu')(hidden1)
concat = keras.layers.Concatenate([input_A, hidden2])
output_aux = keras.layers.Dense(1)(hidden2)
output_main = keras.layers.Dense(1, name="output")(concat)
model = keras.Model(inputs=[input_A, input_B], outputs=[output_main, output_aux])
```

### Saving and restoring a model
```python
model.save("my_keras_model.h5")
model = keras.models.load_model("my_keras_model.h5")
```

### Callbacks
Important if say you need to save checkpoints of a neural network.
```python
checkpoint_cb = keras.callbacks.ModelCheckpoint("my_keras_model.h5")
history = model.fit(X_train, y_train, epochs=10, callbacks=[checkpoint_cb])
```
 With cross validation you can add an extra parameter to save the best model
 ```python
checkpoint_cb = keras.callbacks.ModelCheckpoint("my_keras_model.h5", save_best_only=True)
history = model.fit(X_train, y_train, epochs=10, callbacks=[checkpoint_cb], validation_data=(X_valid, y_valid))
```

Another way to implement early stopping is a callback function like below
Patience is the epochs is waits until making a decision
```python
early_stopping_cb = keras.callbacks.EarlyStopping(patience=10, restore_best_weights=True)
history = model.fit(X_train, y_train, 
                    epochs=100, 
                    callbacks=[checkpoint_cb, early_stopping_cb])
```

Custom Callbacks
```python
class PrintValTrainRatioCallback(keras.callback.Callback):
    def on_epoch_end(self, epoch, logs):
        print("\nval/train: {:.2f}".format(logs["val_loss"]/logs["loss"]))
```

## Tensorboard for visualizations
This does it all. To see output in it you must output the data you want to visualize to binary files called event files. Each binary data record is called a summary. 

different sub directory for each run
```python
import os
import time
root_logdir = os.path.join(os.curdir, "my_logs")

def get_run_logdir():
    run_id = time.strftime("run_%Y_%m_%d_%H_%M_%S")
    return os.path.join(root_logdir, run_id)

run_logdir = get_run_logdir()
tensorboard_cb = keras.callbacks.TensorBoard(run_logdir)
history = model.fit(X_train, y_train,
                   epochs=30,
                   validation_data=(X_valid, y_valid),
                   callbacks=[tensorboard_cb])
```

```bash
tensorboard --logdir=./my_logs, --port=6006
```
then go to http://localhost:6006
