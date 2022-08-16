## Softmax
Binary Classification
$$\LARGE\begin{align}
&\text{Logistic Regression}\\
&z = \vec{w}\cdot\vec{x}+b \\
&a_1 = g(z) = \frac{1}{1+e^{-z}}=p(y=1|\vec{x}) \\
&a_2 = 1 - a_1= p(y=0|\vec{x})
\end{align}$$
$$\LARGE
\begin{align}
&\text{Softmax Regression - 4 possible outputs}\\
& z_j = \vec{w}_j\cdot\vec{x}+b_j \\ 
& a_j = \frac{e^{z_j}}{\sum^N_{k=1}e^{z_k}} \\
& a_j = p(y = j|\vec{x}) \\
& a_1 + \cdots + a_n = 1
\end{align}$$

Parameters for softmax regression are $w1,\dots, w_n$ & $b_1,\dots,b_n$

## Loss Function
$$loss(a_1,\dots,a_N,y) = \left\{\begin{matrix}
-log \hspace{0.2 em}a_1, & if \hspace{0.4 em}y = 1\\ 
-log \hspace{0.2 em}a_2, & if \hspace{0.4 em}y = 2\\ 
 \vdots \\ 
-log \hspace{0.2 em}a_N, & if \hspace{0.4 em}y = N 
\end{matrix}\right.$$
## Softmax N.N. Implementation
The main thing that needs to change isn't the hidden layers but the output layer.
We will have a softmax layer with N outputs one for each class. 

Something unique about softmax is the z's are used simulaeneously together
```python
import tensorflow as tf
from tf.keras import Sequential
from tf.keras.layers import Dense
model = Sequential([
					Dense(units=25,activation='relu'),
					Dense(units=15,activation='relu'),
					Dense(units=10,activation='softmax'),
])
```

#### Softmax loss function
```python
from tf.keras.losses import SparseCategoricalCrossentropy
model.compile(loss= SparseCategoricalCrossentropy)
```

## Fixing Logistic Regression
Before we fix softmax we must update logistic regression
In logistic regression we typically use the loss function below that takes a as a parameter
$$loss=-ylog(a)-(1-y)log(1-a)$$
The problem though is numerical roundoff a solution is to rather expand a and make loss a function of z
$$loss=-ylog(\frac{1}{1+e^{-z}})-(1-y)log(1-\frac{1}{1+e^{-z}})$$
rather than 
```python
model.compile(loss=BinaryCrossEntropy)
```
use
```python
model.compile(loss=BinaryCrossEntropy(from_logits=True) )
```

## Now for softmax
Now what we are doing is using the NN to calculate the Z's of the function
```python
import tensorflow as tf
from tf.keras import Sequential
from tf.keras.layers import Dense
model = Sequential([
					Dense(units=25,activation='relu'),
					Dense(units=15,activation='relu'),
					Dense(units=10,activation='linear'), # This is now linear
])
model.compile(loss=SparseCategoricalCrossEntropy(from_logits=True) )
model.fit(X,Y,epochs=100)
logits = model(X)
f_x = tf.nn.softmax(logits).numpy()
# The max can also be found by doing
np.argmax(logits)
```

