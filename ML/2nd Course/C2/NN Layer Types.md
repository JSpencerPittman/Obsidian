## Dense
Each neuron output is a function of all the activations outputs of the previous layer
$$\vec{a}^{|2|}_1 = g(\vec{w}^{|2|}_1\cdot\vec{a}^{|1|}+b^{|2|}_1)$$
## Convolutional Layer
Each neuron only sees a partial amount of the input data of the previous layer

**Why?**
Speeds up computation
Needs less training data (less prone to overfitting)
