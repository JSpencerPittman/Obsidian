# Evaluate Anamoly Detection Algorithm
Fit $P(x)$ to $x_{train}$
Predict on $x_{cv} \hspace{0.25 em} and \hspace{0.25em} x_{test}$
$$
y = \left\{\begin{matrix}
1, \text{if } p(x) < \epsilon \text{ anamoly}\\ 
0, \text{if } p(x) \geq \epsilon \text{ anamoly}
\end{matrix}\right.
$$
Then you need to choose an evaluation metric
	Precision/Recall?
	$F_1$ Score?

Use $x_{cv}$ to choose ideal $\epsilon$

Anamoly | Supervised
-- | --
Few + examples & many - examples | Large number of - & + examples
Different "Types" of anamolies | Get a sense of what a + sample looks like

### How to fix features for anamoly detection
If a distribution of the data appears skewed to a side use the log of that feature to get a more normal looking distibution

You can also do $log(x+c)$, $\sqrt{x}$, $x^{\frac{1}{3}}$

Try creating features from prexisting ones to better distinguish differences between anamolous and normal examples.

## Error Analysis
We want $p(x)$ large for normal examples x
We want $p(x)$ small for anamoly examples x

A common problem is that $p(x)$ is large for normal & anomoulus examples


