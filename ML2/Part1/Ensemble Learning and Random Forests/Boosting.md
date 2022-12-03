# Boosting
AKA "hypothesis boosting"
Any ensemble method that can combine several weak learners into a strong learner.
The general idea of boosting methods is to train predictors sequentially, each trying to correct its
	predecessor.
Most popular are AdaBoost(Adaptive Boosting) and Gradient Boosting

### AdaBoost
To correct its predecessor the new predictor pays attention to the training instances that the predecessor underfitted. This results in predictors focusing more and more on hard cases. 

Again it trains a base classifier and uses it to make predictions on the training set. The algorithm then increases the relative weights of missclassified training instances and trains a second classifier using the updated weights.
Similar to gradient descent but instead of tweaking a single predictors parameters to minimize a cost function adaboost adds predictors to the ensemble. 

A drawback though is that it can't be parallelized. 

*Equation 7-1. Weighted error rate of the jth predictor*
$$\LARGE r_j=\frac{\underset{\hat{y}^{(i)}_j\neq y^{(i)}}{\sum^m_{i=1}}w^{(i)}}{\sum^m_{i=1}w^{(i)}}$$
> $\hat{y}^{(i)}_j$ is the prediction for the ith training example on the jth training set

The more accurate the predictor the higher its weight $\alpha_j$ while random will be around $0$. Most often wrong will be negative. 
*Equation 7-2. Predictor Weight*
$$\LARGE \alpha_j=\eta\hspace{0.2 em}log\frac{1-r_j}{r_j}$$
> $\eta$ is the learning rate hyperparameter

Next the AdaBoost algorithm updates the instance weights using the following equation which boosts the weights of misclassified instances
*Equation 7-3. Weight update rule*
$$\LARGE w^{(i)}=\left\{\begin{matrix}
w^{(i)}&\text{ if }\hat{y}_j^{(i)}=y^{(i)}\\ 
w^{(i)}exp(\alpha_j)&\text{ if }\hat{y}_j^{(i)}\neq y^{(i)}\\ 
\end{matrix}\right.$$
Then all instance weights are normalized (divided by $\sum^m_{i=1}w^{(i)}$)

Then a new predictor is trained using the new weights and the process continues until either the desired amount of predictors are found or the perfect predictor is found. For predictions adaboost uses the corresponding $\alpha_j$ of each predictor and weighs the predictions of each predictor. 

*Equation 7-4. AdaBoost Predictions*
$$\LARGE\hat{y}(X)= \underset{k}{argmax}\underset{\hat y_j(X)=k}{\sum^N_{j=1}}\alpha_j$$
> $N$ number of predictors

Scikit-learn uses a multi-class version of AdaBoost called SAMME(Stagewise Additive Modeling using a Multiclass Exponential Loss Function) When there are two classes SAMME is equivalent to AdaBoost. If the predictors can estimate class probabilities then we use a variant of SAMME called SAMME.R (R stands for "Real") which relies on class probabilities rather than predictions and generally performs better.

If overfitting regularize baseclassifiers or reduce amount of estimators.

### Gradient Boosting
Works like AdaBoost in that it also sequentially trains its predictors, each one correcting its predecessor. Instead of tweaking instance weights at every iteration like AdaBoost, this method tries to fit the new predictor to the *residual errors* made by the previous predictor.

**Residual Error**
Difference between expected and predicted

**Gradient Tree Boosting** or **Gradient Boosted Regression Tree (GBRT)**
Use decision trees as the base predictors.

We plug in the residual error for y with each training set. 
Y_pred is the sum of each models output.

**Shrinkage**
By shrinking the learning parameter will require more trees but the predictions will often generalize better.

Early stopping is often a good technique to stop overfitting. 
Staged_predict() can help with this

Using random subsets of the training set is called *Stochastic Gradient Boosting*

XGBoost optimized version of gradient descent.

previous:
[[Random Forests]]
next:
[[Boosting]]