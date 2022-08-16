# Training a Neural Network
L = layers of neural network
$S_j$ = neurons in layer j
$(h_\theta(x^{(i)}))_k$ = kth output for example i from the hypothesis

### Cost function of a neural network
$$J(\Theta) = -\frac{1}{m}\sum^{m}_{i=1}\sum^{K}_{k=1}y^{(i)}_klog((h_\theta(x^{(i)}))_k)+(1-y^{(i)}_k)log(1-(h_\theta(x^{(i)}))_k) + \frac{\lambda}{2m}\sum^{L-1}_{l=1}\sum^{S_l}_{i=1}\sum^{S_{(l-1)}}_{j=1}(\theta^{(l)}_{ji})^2$$
This may seem really complex but that's only because there's more classes and weights. This logic is nothing new it's just using more parameters and output classes.

**So how do we minimize this cost function?**
To do this we now we need to use back propogation instead of gradient descent.

To do this we first need the $J(\Theta)$ and $\frac{\partial J(\Theta)}{\partial \theta^{(l)}_{ij}}$ which is the partial derivative of the cost function with respect to each $\theta$.

## Backpropogation
An important variable is the **error**. This will be shown as $\delta ^{(l)}_j$ which is the error of node i in layer l. For the output layer the error is
$$\begin{align}
\delta^{(l)}_j &= a^{(l)}_j - y_j \\
\delta^{(l)} &= a{(l)} - y
\end{align}$$

Where $l$ is the final layer of the neural network.

Heres the error for the hidden layers
$$\begin{align}
\delta^{(l)} &= (\theta^{(l)})^T\delta^{(l+1)}.*g'(z^{(l)}) \\
g'(z^{(l)}) &= a^{(l)}.*(1-a^{(l)}) \\
\delta^{(l)}_j &= (\theta^{(l)})^T_j\delta^{(l+1)}.*(a^{(l)}_j.*(1-a^{(l)}_j)) \\
\end{align}$$

There's no $\delta^{(1)}$ because this would mean there's an error on the input which would be illogical.

## Derivative of the cost function $J(\Theta)$
$$\frac{\partial}{\partial \theta^{(l)}_{ij}}J(\theta) = a^{(l)}_j\delta^{(l+1)}_i$$
## Algorithm for Backpropogation
First initialize the training set and delta

$$\begin{align}
&\{(x^{(1)},y^{(1)}),\cdots,(x^{(m)},y^{(m)})\}\text{ Training Set}\\
&\Delta^{(l)}_{ij} = 0 \text{ (for all } l,i,j\text{)}
\end{align}$$
Then for i = 1 to m do this
$$\begin{align}
&a^{(1)} = x^{(i)} \\
&\text{Perform Forward Propogation to compute }a^{(l)} \text{ for }l = 2,3,\cdots,L\\
&\text{Use } y^{(i)} \text{ to compute } \delta^{(L)} = a^{(l)}-y^{(i)}\\
&\text{Compute } \delta^{(l-1)},\delta^{(l-2)},\cdots,\delta^{(2)}\\
&\Delta^{(l)}_{ij} = \Delta^{(l)}_{ij} + a^{(l)}_j\delta^{(l+1)}_i \text{ or } \Delta^{(l)} := \Delta^{(l)} + \delta^{(l+1)}(a^{(l)})^T
\end{align}$$

Then finally do
$$\begin{align}
&D^{(l)}_{ij} := \frac{1}{m}\Delta^{(l)}_{ij} + \lambda\theta^{(l)}_{ij} (\text{if }j \neq 0)\\
&D^{(l)}_{ij} := \frac{1}{m}\Delta^{(l)}_{ij} (\text{if }j =0)\\
&\frac{\partial}{\partial\theta^{(l)}_{ij}}J(\Theta) = D^{(l)}_{ij}
\end{align}$$

