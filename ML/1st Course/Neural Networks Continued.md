# Neural Networks Cont.
## Gradient Checking
Sometimes in back-propogation it may look like a cost is decreasing but the error may be increasing. Gradient checking solves this.
To approximate the derivative of $J(\Theta)$ you would calculate:
$$\frac{dJ(\Theta)}{d\theta} \approx \frac{J(\theta+\epsilon)-J(\theta-\epsilon)}{2\epsilon}$$
Now if $\Theta = [\theta_1,\theta_2,\cdots,\theta_n]\epsilon \mathbb{R}^n$ Then:
$$\frac{dJ(\Theta)}{d\theta} \approx \frac{J(\theta_1,\theta_2,\cdots,\theta_n+\epsilon)-J(\theta_1,\theta_2,\cdots,\theta_n-\epsilon)}{2\epsilon}$$
Then check if the approximation $\approx$ D vector.
## Random Initialization
To Create a neural network we need out $\Theta$'s to equal something. This is what random Initialization's for. But the $\Theta$'s in a layer need to be different so the activation functions aren't identical. So Initialize each $\theta^{(l)}_{ij}$ to a random value in $[-\epsilon, \epsilon]$. The code for this would actually be  `[rand(r,c) x (2ε)]-ε`



