# Fine-Tuning Neural Network Hyperparameters
One option is to use GridSearchCV or RandomizedSearchCV

First create a function that builds and compiles a Keras model given certain hyperparameters for exampel the one below fulfills this.
```python
def build_model(n_hidden=1, n_neurons=30, 
                learning_rate=3e-3, input_shape=[8]):
        model = keras.models.Sequential()
        model.add(keras.layers.Input(input_shape=input_shape))
        for layer in range(n_hidden):
            model.add(keras.layers.Dense(n_neurons, activation='relu'))
        model.add(keras.layers.Dense(1))
        optimizer = keras.optimizers.SGD(lr=learning_rate)
        model.compile(loss="mse", optimizer=optimizer)
        return model
```

Next we'll create a KarasRegressor which is a thin wapper around the keras model built using build_model, this will allow it to be trained like a regular scikit-learn regressor
```python
keras_reg = keras.wrappers.sci_kit_learn.KerasRegressor(build_model)
```

An example of an evaluation may look like below
```python
keras_reg.fit(X_train, y_train, epochs=100,
              validation_data=(X_valid, y_valid),
              callbacks=[keras.callbacks.EarlyStopping(patience=10)])
mse_test = keras_reg.score(X_test, y_test)
y_pred = keras_rwg.predict(X_new)
```

techniques to explore a search space efficently and not as badly as random
Good regions should be explored more
Good libraries that help
- Hyperopt
- Hyperas, kopt, Talos
- Keras Tuner
- Scikit-Optimize (skopt)
- Spearmint
- Hyperboard
- Sklearn-deep
Evolutionary algorithms are coming back to help with this.

## Number of hidden layers
Deep neural networks have a much higher parameter efficency that shallow ones
This is because neural networks take advantage of the hiearchial nature of data in the real world. 

Transfer learning allows you to kickstart your training with an algorithm already attuned to recognized lines and objects. In many instances one or two layers works just fine. For more complex problems keep adding more layers until it overfits the dataset. 

## Number of neurons per hidden layer
Determined by type of input and output task requires. Often a pyramid is used under the idea many low-level features may coalesce in fewer high-level features. 
Although it has been observed that a consistent amount of neurons often performs as well if not better than the pyramid scheme also leaving one hyperparameter to tune in this respect. 

Often its best to overkill with layers and neurons and use early stopping to prevent overfitting. "Stretch Pants" approach. 

Best to add more layers not neurons per layer.

## Learning Rate, Batch Size, and other
**Learning Rate**
Optimum learning rate is often half the max learning rate. The max learning rate is where the algorithm diverges.

One approach is to train the model for a few hundred iterations, starting very low say ($10^{-5}$) and gradually increasing up to a large value ($10$). You can do this by gradually increasing the learning rate by a constant factor at each iteration to from from low to high. 
Example would be to go from $10^{-5}$ to $10$ in in 500 iterations by a scale factor of $log(10^6)/500$ and just use a log scale as the learning rate. Optimal is a bit lower than before the point starts to climb up from being to large, often about 10 times lower than the turning point. 

**Optimizer**
Choosing these are important

**Batch Size**
Large batch sizes are processed efficently by gpu's so the training algorithm gets more instances done per second, however large batch sizes often lead to training instabilities especially in the beginning and reduce generalization. Small batches from 2-32 are often more accurate. 

Although a large batch size with learning rate warmup can work, if it doesn't you can always try a different approach.

**Activation Function**
Often the ReLU function will be just fine for your task

**Number of iterations**
Often you don't need to tweak this rather just employ early stopping

Optimal learning rate relies on other hyperparameters, make sure to update both not just one in isolation of the other.


