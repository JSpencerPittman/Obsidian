# Neural Networks Summary
## 1. Pick an Architecture
This entails the # of Inputs AKA Dimension of features $x^{(i)}$
The # of outputs AKA Number of classes
At least one hidden layer so that $L \geq 3$ "The more the better"

## 2. Implement a Neural Network
Randomly Initialize Weights
Implement Forward Propogation to get $h_\theta(x^{(i)})$ for any $x^{(i)}$
Implement Code to calculate $J(\Theta)$
Implement Back-Propogation to complete partial derivatives $\frac{\partial}{\partial\theta^{(l)}_{ij}}J(\Theta)$
## 3. Train a Neural Network
Gradient check computed $\frac{\partial}{\partial\theta^{(l)}_{ij}}J(\Theta)$ with numerical estimate of $J(\Theta)$ then disable Gradient
	Checking code once it works
Use Gradient Descent or some other method to minimize $J(\Theta)$

## Pros and Cons of Neural Network Sizes
Small | Large
--- | ---
Computationally Cheap | Computationally expensive
Underfitting | Overfitting (can be helped with regularization)
