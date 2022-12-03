# Polynomial Regression
For this type of thing try to use degrees above one for features as well
Scikit's PolynomialFeatures class is great for this. Polynomial accounts better for variable corellations because it multiplies them together as well. 
$$\LARGE a+b\rightarrow a+ b+a^2+ab+b^2$$
If degree equals $d$ then the number of features created by doing this is 
$$\LARGE\frac{(n+d)!}{d!n!}$$
## Learning Curves
A function of model's performance with respect to training iteration or training set size. 
 Use these to analyze whether or not model is over fitting or underfitting the data. 