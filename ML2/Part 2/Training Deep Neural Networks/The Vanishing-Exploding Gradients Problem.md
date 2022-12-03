# The Vanishing/Exploding Gradients Problem
**Vanishing Gradients Problem**
In backproprogation once the error gradients been proprogated across the network, and has calculated the gradient of the cost function with regard to every parameter in the network, it uses these to update each parameter in a gradient descent step. The gradients however get smaller and smaller in the lower layers leaving the lower layers connection weights virtually unchanged making training never converge to a final solution. 

**Exploding Gradients Problem**
The opposite happens and the network starts to diverge from a solution. 
Often happens in recurrent neural networks.

*Gradient's Instability*
Often DNN's suffer from unstable gradients; different layers learn at very different speeds. 
Some causes were found to be the combination of the sigmoid activation function and the weight initialization technique used at the time-(normal distribution, mean=0, std=1), with this design the variance of the outputs of each layer is much greater than the variance of its inputs. This keeps getting worse with each layer, the logistic function's mean is 0.5 which doesn't help. When inputs become large they get saturated at 0 and 1, with a derivative extremly close to 0. Whatever gradient does exist gets diluted very fast. 

## Glorot and He Initialization
Signal needs to flow in both forward and backwards directions.
Therefore the variance of the outputs of each layer must equal the variance of the inputs to that layer. 
The gradients also need to have equal variance before and after each layer in the reverse direction.
The conneciton weights must be initialized randomly as described in the following equation.

*Equation 11-1. Glorot Initialization (when using the logistic activation function)*
$$
\LARGE\begin{align}
&\text{Normal distribution with mean 0 and variance }\sigma^2=\frac{1}{fan_{avg}}\\
&\text{Or a uniform distribution between $-r$ and $+r$, with }r=\sqrt{\frac{3}{fan_{avg}}}
\end{align}$$
> $fan_{avg}=(fan_{in}+fan_{out})/2$ 
> $fan_{out}$ number of outputs
> $fan_{in}$ number of inputs

LeCun initialization is the same as Glorot Initializationif you replace $fan_{avg}$ with $fan_{in}$ 

In the following table just do $r=\sqrt{3\sigma^2}$ for the uniform distribution

The initialization strategy for ReLU is called the He Initialization.

**Initialization parameters for each type of activation function**
Initialization | Activation Function | $\sigma^2$(normal)
-- | -- | --
Glorot | None, tanh, logistic, softmax | $1/fan_{avg}$
He | ReLU and variants | $2/fan_{in}$
LeCun | SELU | $1/fan_{in}$

## Nonsaturating Activation Functions
ReLU often works far better in DNN's due to not saturating positive values and faster to compute. 
Although ReLU suffers from "dying ReLUs" as in during training some neurons die and just don't put anything except 0 out. 

A variant of the ReLU function solves this that's called Leaky ReLU
$LeakyReLU_\alpha(z)=max(\alpha z, z)$
Here $\alpha$ is a hyperparameter that determines how much it leaks. It's the slope of the function for when $z < 0$
and is  typically around 0.01 allows long comas and doesn't tolerate permanent death. In fact larger leaks often were more effective than small leaks which in turn were more effective than standard ReLU functions. 
RReLU (randomized leaky ReLU) is where $\alpha$ is picked randomly and uses average in testing
	acts as a regularization parameter also
PReLU (parametric leaky ReLU) where $\alpha$ is authorized to be learned during training becomes a parameter rather 
	than hyperparameter for bp.
	works best on larger datasets

ELU (Exponential Linear Unit)
Outperformed all ReLU variants
*Equation 11-2. ELU activation function*
$$\LARGE ELU_\alpha(z)=\left\{\begin{matrix}
\alpha(exp(z)-1)&\text{ if $z < 0$}\\ 
z&\text{ if $z \geq 0$}
\end{matrix}\right.$$
Similar to ReLU but when $z < 0$ the average output is closer to 0 which helps alleviate the vanishing gradients problem. $\alpha$ is the value z approaches when its a large negative number although usually its 1.
Nonzero gradient as $z$ avoiding the dead neuron problem. 
Although it's slower to compute than ReLU and its variants. 
Few iterations compensates for training but not live testing calculations.

However the Scaled ELU (SELU) is a scaled variant of the ELU function. If you create a stack of dense layers and if all hidden layers use SELU then the network will *self-normalize* the output of each layer will tend to preserve a mean of 0 and standard deviation of 1. This solves the gradients problem. The requirements for this is 
- The input features must be standardized (mean 0 and std of 1)
- All hidden layers must use LeCun intialization
- Sequential network architecture
In these conditions it outperforms its competitors

In general precedence should be as follows
SELU > ELU > Leaky ReLU (and variants) > ReLU > tanh > logistic

### Batch Normalization
While He and ELU can significantly reduce the danger of the vanishing/exploding gradients problems at the beginning of training, it doesn't guarantee that they wont come back during training. 
This is where batch normalization comes in. 
Adds an operation in the model just before or after the activation function of each hidden layer. This operation zero-centers and normalizes each input and scales and shifts the rsults using two new parameter vectors per layer one for scaling and the other for shifting. 

Often a BN layer as the first layer replaces the need to scale your input features 
*Equation 11-3. Batch Normalization algorithm*
$$\LARGE\begin{align}
&\mu_b=\frac{1}{m_B}\sum^{m_B}_{i=1}x^{(i)}\\
&\sigma_B^2=\frac{1}{m_B}\sum^{m_b}_{i=1}(x^{(i)}-\mu_B)^2\\
&\hat x^{(i)}=\frac{x^{(i)}-\mu_B}{\sqrt{\sigma^2_B+\epsilon}}\\
&z^{(i)}=\gamma\otimes\hat x^{(i)}+\beta
\end{align}$$
> $\otimes$ is element-wise multiplication
> $\gamma$ is the output scale parameter vector ($m_B$ x 1)
> $\beta$ is the output shift (offset) parameter vector for the layer
> $\epsilon$ is a tiny number that avoids division by zero AKA a smoothing term
> $\hat x^{(i)}$ is the vector of the zero-center and normalized inputs for instance $i$ 
> $Z^{(i)}$ is the output of the BN operations. It is rescaled and shifted versions of the output

A problem occurs at runtime when we don't have a batch to calculate mean and variation on. 
One solution could be to train the network and then calculate mean and standard deviation of each bn layer. 
Although most implementations will just use a moving average of the input layers means and standard deviations. 
$\gamma$ and $\beta$ are learned through backpropogation
$\mu$ and $\sigma$ are estimated during training but used only after training. 

In addition the vanishing gradient problem became very reduced. The networks were less sensitive to the weight initialization. In addition they also uses much larger learning rates. In addition batch normalization acts as a regularization technique. 

However complexity is added to the model and runtime computations make slower predictions. Luckily its possible to fuse the BN layer with the previous layer after training. You do this by updating the previous layer's weights and biases so that it directly produces outputs of the appropiate scale and offset. 

often BN training is slow but it converges faster counterbalancing the bad. 
Add it before or after each layer. 

```python
model = keras.models.Sequential([
	Flatten(input_shape=[28,28]),
	BatchNormalization(),
	Dense(300, activation='elu', keras_initializer="he_normal"),
	BatchNormalization(),
	Dense(100, activation='elu', keras_initializer="he_normal"),
	BatchNormalization(),
	Dense(10, activation='softmax')
])
```

The improvements made by BN are more noticeable in deeper neural networks. 

We can combine layers following the logic below:
The previous layer computers $XW+b$
The BN layer computes $\gamma\otimes(XW+b-\mu)/\sigma+\beta$ 
But if we say $W'=\gamma\otimes(W)/\sigma$ 
and $b' =\gamma\otimes(b-\mu)/\sigma+\beta$
Then the layers can be combined as $XW'+b'$ 

If you put a BN before an activation function make sure to turn off bias as an offset has already been introduced. 