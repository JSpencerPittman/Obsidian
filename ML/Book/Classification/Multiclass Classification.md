# Multiclass Classification
Some systems are natively multiclass classifiers other's are restricted to binary and must be trained individually for each class(OvR) or train them in pairs as (OvO)

To force scikit-learn to use OvO or OvR you need to use
`OneVsOneClassifier(estimator)` or `OneVsRestClassifier(estimator)`

Use a confusion matrix to view the predictions and also matshow to display them
