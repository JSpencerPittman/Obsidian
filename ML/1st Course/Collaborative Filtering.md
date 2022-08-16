# Collaborative Filtering
Algorithm that learns for itself what features to utilize

Here were trying to find our x features

### Optimization Algorithm

Given $\theta^{(1)},\theta^{(2)},\cdots,\theta^{(n_u)}$, to learn $x^{(i)}$:
$$\underset{x^{(i)}}{min}\frac{1}{2}\sum_{i:r(i,j)=1}((\theta^{(j)})^T(x^{(i)})-y^{(i,j)})^2 + \frac{\lambda}{2}\sum^n_{k=1}(x_k^{(i)})^2$$
Given $\theta^{(1)},\theta^{(2)},\cdots,\theta^{(n_u)}$, to learn $x^{(1)},\cdots,x^{(n_m)}$:
$$\underset{x^{(1)},\cdots,x^{(n_m)}}{min}\frac{1}{2}\sum^{n_m}_{i=1}\sum_{i:r(i,j)=1}((\theta^{(j)})^T(x^{(i)})-y^{(i,j)})^2 + \frac{\lambda}{2}\sum^{n_m}_{i=1}\sum^n_{k=1}(x_k^{(i)})^2$$
**So X or $\Theta$ first?**
The x's give us $\theta$
and the $\theta$'s give us x

Guess $\Theta$ -> x -> $\theta$ -> x -> $\theta$ -> $\cdots$

To combine $\theta$ and x into one we use this optimization objective
$$\begin{align}
&J(x^{(i)},\cdots,x^{(n_m)},\theta^{(1)},\cdots,\theta^{(n_u)})=\\
&\frac{1}{2}\sum_{(i,j):r(i,j)=1}((\theta^{(j)})^Tx^{(i)}-y^{(i,j)})^2 +\frac{\lambda}{2}\sum^{n_m}_{i=1}\sum^n_{k=1}(x^{(i)}_k)^2+\frac{\lambda}{2}\sum^{n_u}_{j=1}\sum^n_{k=1}(\theta^{(j)}_k)^2\\
&\underset{\theta^{(1)},\cdots,\theta^{(n_u)}}{\underset{x^{(1)},\cdots,x^{(n_m)}}{min}}J(x^{(i)},\cdots,x^{(n_m)},\theta^{(1)},\cdots,\theta^{(n_u)})
\end{align}$$

## Collaborative Filtering Algorithm
1. Initialize $x^{(1)},\dots,x^{(n_m)}$ and $\theta^{(1)},\dots,\theta^{(n_u)}$ to small random values
2. Minimize $J(x^{(1)},\dots,x^{(n_m)},\theta^{(1)},\dots,\theta^{(n_u)})$ using gradient descent for every $j=1,\dots,n_u,i=1,\dots,n_m:$ 
$$\begin{align}
&x^{(i)}_k:=x^{(i)}_k-\alpha\sum_{j:r(i,j)=1}((\theta^{(j)})^T(x^{(i)})-y^{(i,j)})\theta^{(j)}_k + \lambda x_k^{(i)}\\
&\theta^{(j)}_k:=\theta^{(j)}_k-\alpha\sum_{i:r(i,j)=1}((\theta^{(j)})^T(x^{(i)})-y^{(i,j)})x^{(i)}_k + \lambda\theta^{(j)}_k\end{align}$$
3. For a user with parameters $\theta$ and learned features $x$ predict a star rating of $\theta^Tx$ 