# Model Selection and T/CV/T Sets
A lot of problems require that there be some sort of degree D. For example how would we choose in a linear regression problem between 
$$h_\theta(x) = \theta_0 + \theta_1x_1 \text{ or } \theta_1x_1 + \theta_2x_1^2 \text{ or }  \theta_1x_1 + \theta_2x_1^2 + \cdots + \theta_{10}x_1^{10}$$
To answer this question we need to create a $\theta^D$ for each degree D. Then perform a test one each and pick the one with the lowest test set error.

While above is fine there's a far more effective war to evaluate algorithms which is similar to having a training and test set but now we include a cross-validation set. 
Here 60% goes to the training set, 20% to validation, and 20% to testing.

### Procedure
1. Train on a training set and get $\theta^{(d)}$
2. Test models on $J_{cv}(\theta^{(d)})$
3. Select lowest $J_{cv}(\theta^{(d)})$ for the model
4. Estimate generalization error with $J_{\text{test}}(\theta^{(d)})$