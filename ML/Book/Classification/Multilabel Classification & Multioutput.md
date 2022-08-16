## Multilabel Classification
A multilabel classification system is one that can recognize multiple objects in the same input. 

For this you can make you y array consist of multiple columns-each thing to identify
and then pass it into the fit as such

we can use f1_score to evaluate our metric as so
```python
from sklearn.metrics import f1_score
f1_score(y_multilabel, y_train_knn_pred, average='macro')
```
Here we use 'macro' because we believe that each label is equally important
If we wish to do it based on whether some classes are more prevalent than others we can do 'weighted' instead which uses their supports.

## Multioutput-Multiclass Classification
Generalization of multi-label classification where each label can have multiple classes

