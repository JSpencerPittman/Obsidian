# Neural Networks
Neural Networks originated from algorithms trying to mimic the human brain. Their named after a primal component of the brain called a neuron-bet you didn't know that. 
![[neuron.jpeg]]

Neural networks share a similar design as it goes like this
![[NeuralNetwork.png]]

Now if you didn't notice we don't have an $x_0$ displayed well first this is called the "biased neuron" and you're just supposed to pretend it's there. Anyways what it does is just retain the value 1 and contribute in every layer except for the output layer.

Also now our typical parameters $\Theta$ will now be considered as "weights".
To finish off our new terminology we now have activation functions whose notation is as follows:
$a^{(j)}_i$ which means an activation of neural i in layer j. The i is the index in its row and j is the index of the row which aren't 0-based. 

In the neural network there are the input layers and output layers-self explanatory-and the hidden layers which is where most of the computations will take in a typical neural network. 

Also one more thing $\Theta^{(j)}$ is the weights that dictate the function mapping from layer j to layer j+1. Also the dimensions of $\Theta^{(j)}$ is $S_{j+1}\hspace{0.25em} X \hspace{0.25em}S_j+1)$. When talking about activation functions we do $a^{(layer)}_{row}$.

The equation for an activation function on layer 2 row 1 is
$$a^{(2)}_1 = g(\theta^{(1)}_{10}x_0 + \theta^{(1)}_{11}x_1 + \theta^{(1)}_{12}x_2 + \theta^{(1)}_{13}x_3)$$
As it can be seen $\theta$ can be broken down as $\theta^{previousRow}_{(activationRow, \hspace{0.25 em}inputRow)}$ and g up above is the sigmoid function. The $\theta^{(1)}_{10}x_0 + \theta^{(1)}_{11}x_1 + \theta^{(1)}_{12}x_2 + \theta^{(1)}_{13}x_3$ can be encapsulated as 
$$Z^{(2)}_1 = \theta^{(1)}_{10}x_0 + \theta^{(1)}_{11}x_1 + \theta^{(1)}_{12}x_2 + \theta^{(1)}_{13}x_3$$
such that:
$$\begin{align}
g(Z^{(2)}_1) &= a^{(2)}_1 \\
g(Z^{(2)}) &= a^{(2)} \\
Z^{(2)} &= \Theta^{(1)}X 
\end{align}$$
To generalize this would be to say:
$$\begin{align}
Z^{(r)} = \Theta^{(r-1)}a^{(r-1)}\\
h_\theta(x) = a^{(r)} = g(z^{(r)}) 
\end{align}$$

## Multiclassification within a neural network
For this there will be an output for each possible class. $h_\theta(x) \epsilon \mathbb{R}^n$. 