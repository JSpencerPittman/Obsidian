# Data Compression
![[linearPlot.png]]
In this plot we can see that the data is being described by two features but we can easily maintain a great portion of that data by storing it as in one dimension corresponding the the blue line. 

Which would create something like so
$$x^{(i)} \epsilon \mathbb{R}^n \rightarrow z^{(i)}\epsilon \mathbb{R}^k$$
This requires that $k \leq n$

### Dimensionality Reduction
We can use principle component analysis to solve this algorithm. We can reduce from n-d9mi to k-dimensions. 

![[linearVsPCA.jpeg]]
On the left is PCA where we check the error of a approximation through it's actual distance while linear regression uses the vertical distance. 