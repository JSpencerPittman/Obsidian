# Stacking
Short for stacked generalization

Instead of using hard voting to aggregate the predictions of all predictors in an ensemble, why don't we train a model to perform this aggregation. The aggregate predictor is called a *blender*/*meta learner*

Training is often done using a holdout set. Split the training into two subsets, the first trains the predictors the first layer. Next the first layers predictors are used to make predictions on the second (held-out) set and the outputs are considered inputs to the second layer model. 

Several Blenders, split the datasets into three subsets: the first one is used to train the first layer, the second one is used to create the training set used to train the second layer and then the third one is used to train the third layer. 

previous:
[[Boosting]]
next: