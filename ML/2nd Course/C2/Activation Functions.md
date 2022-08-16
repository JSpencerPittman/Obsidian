## Alternatives to sigmoid activation
ReLU = $g(z) = max(0,z)$
Linear = g(z) = z

**How to choose?**
Sigmoid is ideal for binary classification
Linear if it should be negative and positive for regression problems
ReLU if it is only nonnegative values for regression problems

**Why is ReLU more widespread?**
Sigmoid is slower to compute
ReLU isn't flat when $Z > 0$ making it faster for gradient descent

## Overall
Sigmoid for binary classification problems
linear for regression problems with +/- values
ReLU for hidden layers and regression problems with $y > 0$
Stay away from the linear function in hidden layers
