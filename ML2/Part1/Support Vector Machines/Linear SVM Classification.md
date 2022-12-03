## Linear SVM Classification
Large Margin Classification is trying to fit the largest street possible into a dataset. This algorithm is fully trained by the parameters on the "edge of the street." These instances are called the support vectors. 

SVM's are very sensitive to feature scales. 

### Soft Margin Classification
Striclty impose that all instances must be off the street and on the right side.
Issues:
1. Only works if the data is linearly separable
2. Sensitive to outliers

Soft margin classification is about compromise between a large street and limiting the margin violations. C is a parameter that is in charge of this balance. A low C promotes generalizability but had more model violations while a high C promotes accuracy.