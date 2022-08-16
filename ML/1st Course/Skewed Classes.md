# Skewed Classes
Some classes are skewed in that the ratio of +'s to -'s is extremely high and in cases like these which are very common we should stay away from using classification accuracy as an error rate.

## Precision/Recall
								Actual
Predicted | 1 | 0
-- | -- | --
1 | True Positive | False Positive
0 | False Negative | True Negative


**Precision**, of all answers guessed to be $y = 1$  what fraction actually were $y = 1$
$$\frac{\text{True Positives}}{\text{No. predicted positives}} = \frac{\text{True Positives}}{\text{True Pos + False Pos}}$$

**Recall**, of all data points where $y = 1$  what fraction did we predict were $y = 1$
$$\frac{\text{True Positives}}{\text{No. Actual positives}} = \frac{\text{True Positives}}{\text{True Pos + False Neg}}$$

Threshold(Increase) = Precision(Increase) = Recall(Decrease)
The threshold is what $h_\theta(x)$ must be greater than to be classified as a one

## $F_1$ Score
$$F_1 \text{ Score: } 2\frac{PR}{P + R}$$
Here $P$ = Precision and $R$ = Recall

$F_1$ has been shown to be more effective than averaging out the scores like so
$$\frac{P + R}{2}$$
