## Adam Algorithm
If the algorithm notices that gradient descent is taking small steps it can alter the learning rate $\alpha$ to bigger leaps and vice versa for leaps that are too big. 

ADAM: Adaptive Moment Estimation

**How does it work?**
Uses a different learning rate for each parameter as shown below
$$\begin{align}
&w_1=w_1-\alpha_1\frac{\partial}{\partial w_1}J(\vec{w},b)\\
&w_2=w_2-\alpha_2\frac{\partial}{\partial w_2}J(\vec{w},b)\\
&b=b-\alpha_3\frac{\partial}{\partial b}J(\vec{w},b)
\end{align}$$

If $w_j$ moves in the same direction increase $\alpha_j$
If $w_j$ keeps oscillating reduce $\alpha_j$

**Code for it only changes for the .compile() step**
```python
model.compile(optimizer=tf.keras.optimizers.Adam(learning_rate=1e-3), loss=tf.keras.losses.SparseCategoricalCrossentropy(from_logits=True))
```
Here we add the optimizer argument and pass in the Adam optimizer