# Recommender Systems
Here we are doing a move example
#### Notation
$$\begin{align}&n_u=\text{no. users}\\&n_m=\text{no. movies}\\&r(i,j)=\text{1 if user j has rated movie i}\\&y^{(i,j)}=\text{rating given by user j to movie i (definded only if r(i,j) = 1)}\end{align}$$
For each movie assign it a feature vector $x^{(i)}$
For each user *j* learn a parameter $\theta^{(j)} \in \mathbb{R}^3$
Predict user *j* as rating movie *i* with $(\theta^{(j)})^Tx^{(i)}$ stars

#### New Notation
$$\begin{align}&\theta^{(j)} = \text{paramer vector for user }j\\&x^{(i)} = \text{feature vector for movie }i\\&\text{For user j, movie i, predicted rating : }(\theta^{(j)})^Tx^{(i)}\\&m^{(j)}=\text{no. movies rated by user }j\end{align}$$
### Cost Function/Optimization Objective 
Here $\theta^{(j)}$ is calculated as follows for user $j$
$$\underset{\theta^{(j)}}{min}\frac{1}{2m^{(j)}}\sum_{i:r(i,j)=1}((\theta^{(j)})^T(x^{(i)})-y^{(i,j)})^2 + \frac{\lambda}{2m^{(j)}}\sum^n_{k=1}(\theta_k^{(j)})^2$$
To learn $\theta^{(1)},\theta^{(2)},\cdots,\theta^{(n_u)}$:
$$\underset{\theta^{(1)},\theta^{(2)},\cdots,\theta^{(n_u)}}{min}\frac{1}{2}\sum^{n_u}_{j=1}\sum_{i:r(i,j)=1}((\theta^{(j)})^T(x^{(i)})-y^{(i,j)})^2 + \frac{\lambda}{2}\sum^{n_u}_{j=1}\sum^n_{k=1}(\theta_k^{(j)})^2$$
## Gradient Descent Algorithm
$$\begin{align}&\theta^{(j)}_k:=\theta^{(j)}_k-\alpha\sum_{i:r(i,j)=1}((\theta^{(j)})^T(x^{(i)})-y^{(i,j)})x^{(i)}_k \text{ (for k = 0)}\\&\theta^{(j)}_k:=\theta^{(j)}_k-\alpha[\sum_{i:r(i,j)=1}((\theta^{(j)})^T(x^{(i)})-y^{(i,j)})x^{(i)}_k + \lambda\theta^{(j)}_k] \text{(for k}\neq\text{0)}\end{align}$$
