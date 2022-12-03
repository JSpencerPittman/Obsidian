# Gaussian Mixtures
Guassian Mixture Model (GMM) is a probablistic model that assumes that the instances were generated form a mixture of several gaussian distributions whose parameters are all unknown. All the instances from a single gaussian distribution form a cluster resembling an ellipsoid. 
Can have differing shape, size, density, and orientation. 

GMM Variants include the simplest of GaussianMixture class but you must know $k$ in advance. 
X is assumed to have been generated through the following probablistic processes. 
- For each instance a cluster is picked randomly from among k clusters. The probability of the jth cluster is defined by the clusters weight $\phi^{(j)}$. The index of the cluster chosen for the ith instance is noted $z^{(i)}$.
- If $z^{(i)}=j$ meaning the ith instance was assigned to the jth cluster the location $x^{(i)}$ of this instance is sampled randomly from the gaussian distribution with mean $\mu^{(j)}$ and covariance matrix $\Sigma^{(j)}$. This is noted$$\LARGE x^{(i)}\sim\mathcal{N}(\mu^{(j)},\Sigma^{(j)})$$
 