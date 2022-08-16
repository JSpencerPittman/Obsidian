# Bias / Variance
![[biasvariance.jpeg]]
Here are the Bias and Variance curves.

We can use this to understand if we have a high bias or high variance problem but its incredibly rare to suffer from both.
![[bv_lcurves.png]]

High Bias | High Variance
----|----
.$J_{\text{train}}(\theta) = High$ | .$J_{\text{train}}(\theta)$ = Low
.$J_{\text{cv}}(\theta) = High$ | .$J_{\text{cv}}(\theta)$ = High
.$J_{\text{train}}(\theta) \approx J_{\text{cv}}(\theta)$ | .$J_{\text{train}}(\theta) << J_{\text{cv}}(\theta)$

### How does $\lambda$ impact regularization
When $\lambda$ is large we see high bias as the parameters are too restricted
On the other hand when $\lambda$ is small we see high variance because the parameters have to
	little restriction.

#### So how do we find the optimal $\lambda$
Just like we did with Degree $D$ cycle through multiple $\lambda$ within a certain range and test them. Get a $\Theta^{(\lambda \text{ value})}$ for each tested/trained $\lambda$. The run a $J_{cv}(\Theta)$ on each one and pick the one with the lowest $\lambda$.


