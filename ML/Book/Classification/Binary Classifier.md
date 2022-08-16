# Performance Measurements
### Example of a cross_val_score implementation
```python
from sklearn.model_selection import StratifiedKFold
from sklearn.base import clone

skfolds = StratifiedKFold(n_splits=3, shuffle=True, random_state=42)

for train_index, test_index in skfolds.split(X_train, y_train_5):
    clone_clf = clone(sgd_clf)
    X_train_folds = X_train[train_index]
    y_train_folds = y_train_5[train_index]
    X_test_fold = X_train[test_index]
    y_test_fold = y_train_5[test_index]
    
    clone_clf.fit(X_train_folds, y_train_folds)
    y_pred = clone_clf.predict(X_test_fold)
    n_correct = sum(y_pred == y_test_fold)
    print(n_correct / len(y_pred))
    
```

Accuracy isn't an ideal performance measure here because the data set is heavily skewed and the distributions of classes are in no way equal, therefore something else must be used. 

## Confusion Matrix
How many times was A confused as B
Look in the Ath row and Bth column to find out

The confusion matrix required a set of predictions and true answers an example is below
```python
from sklearn.metrics import confusion_matrix
from sklearn.model_selection import cross_val_predict

y_train_pred = cross_val_predict(sgd_clf, X_train, y_train_5, cv=3)

confusion_matrix(y_train_5, y_train_pred)
```

Each row is an *actual class* while each column is a *predicted* class

## Threshold Precision/Recall
You may want to manipulate the confidence threshold to utilize the precision/recall tradeoff
Many classifiers will have a `.decision_function()` method enabled allowing you to do just this. It returns a confidence score for a picture.
We can get a list of scores using cross_val_predict from above
```python
y_train_pred = cross_val_predict(sgd_clf, X_train, y_train_5, cv=3, method="decision_function")
```

## Graph Precision Recall Curve
```python
from sklearn.metrics import precision_recall_curve

precisions, recalls, thresholds = precision_recall_curve(y_train_5, y_scores)
```

And just graph precisions and recalls with respect to thresholds for two seperate line plots

![[prec_recall_table_2.png]]

## Custom Threshold
```python
y_scores = cross_val_predict(sgd_clf, X_train, y_train_5, cv=3, method="decision_function")

thresholds_90_precision = thresholds[np.argmax(precisions >= .9)]
y_train_pred_90 = (y_scores >= thresholds_90_precision)
print(precision_score(y_train_5, y_train_pred_90))
recall_score(y_train_5, y_train_pred_90)
```


## ROC Curve
**Reciever Operating Characteristic(ROC)**
Similar to the precision/recall curve but instead of precision versus recall, the ROC plots *true positive rate* (AKA recall) against the *false positive rate* (FPR). FPR is the ratio of negative instances that are incorrectly classified as positive which is equal to $1 - True Negative Rate(TNR)$ 

The y-axis TPR is how many + points are correctly identified
The x-axis FPR is how many - points are incorrectly classified
Ideal is the top-left point for perfection

The Area under curve(AUC) should be as close to 1 as possible while random has a auc of 0.5.

Create an ROC curve thiss way
```python
from sklearn.metrics import roc_curve
fpr, tpr, thresholds = roc_curve(y_train_5, y_scores)
```
and just plot the tpr as y, and fpr as x

Calculate the AUC by doing

### How to choose between ROC/AUC and P/R Curves
P/R if (+ class is rare) or (false positives are more important than false negatives)
ROC/AUC otherwise