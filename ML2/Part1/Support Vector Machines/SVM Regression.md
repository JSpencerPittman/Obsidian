# SVM Regression
Supports linear and nonlinear regression. The trick of applying SVM to regression instead of classification is reversing the objective. Now rather than fitting the largest possible street between two classes while limiting margin violations, SVM Regression tries to fit as many instances as possible on the street while limiting margin violations. The width of the street is controlled by the hyperparameter $\epsilon$. The street is $\epsilon$ insensitive as the width of the street has no effect whatsoever. 

LinearSVR is great for linear regression.
SVR for nonlinear regression which is the regression equivalent of SVC. 

Both SVR and SVC scale poorly with large datasets.