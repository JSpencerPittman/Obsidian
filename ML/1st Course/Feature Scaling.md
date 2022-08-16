# Feature Scaling
In learning algorithms it's often optimal to have the features to be smaller and within the same ranges of each other for faster and more effective learning. This is where feature scaling comes in. Feature scaling is the action of scaling down or up features such that they all fit on a similar scale. A typical one is $-1 \leq x_i \leq 1$.

One approach is to divide the feature by its max, $\frac{x_i}{max(x_i)}$
or perhaps mean normalization where $\mu_i$ = mean of a feature and $s_i$ = range of the feature $x_i$. $${x}' = \frac{x_i - \mu_i}{s_i}$$


