# Anamoly Detection
In anomly detection we set some value $\epsilon$ such that if
$$p(x_{test}) < \epsilon$$ then we flag $x_{test}$ as an anamoly. Otherwise $p(x_{test}) \geq \epsilon$ then it's normal.

### Algorithm
Choose $x_i$ features indicative of anamolies
Fit parameters $\mu_1,\cdots,\mu_n$ and $\sigma^2_1,\cdots,\sigma^2_n$
$$\begin{align}&\mu_j = \frac{1}{m}\sum^m_{i=1}x^{(i)}_j\\&\sigma^2_j=\frac{1}{m}\sum^m_{i=1}(x^{(i)}_j-\mu_j)^2\end{align}$$
Given next example $x$, compute $p(x)$, here p(x) is the gaussian distrobution
$$\begin{align}p(x)&=\Pi^n_{j=1}p(x_j;\mu_j,\sigma^2_j)\\&=\Pi^n_{j=1}\frac{1}{\sigma\sqrt{2\pi}}e^{-\frac{(x_j-\mu_j)^2}{2\sigma^2_j}}\end{align}$$
That fraction in the top right portion is
$$-\frac{(x_j-\mu_j)^2}{2\sigma^2_j}$$
It's an anomly if $$p(x) < \epsilon$$
