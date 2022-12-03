# Voting Classifiers
Suppose you have trained a few classifiers each achieving about 80% accuracy. 
You combine these classifiers to aggregate the predictions of each classifier and predict the most voted class, this majority-vote classifier is called a *hard voting* classifer.

Even if each classifier is a *weak learner* (slightly better than random) the ensemble can still be a *strong learner* (achieving high accuracy), provided there are a sufficent number of weak classifiers and they're sufficently diverse. This phenomena can be attributed to the law of large numbers. 

Although often these weak classifiers aren't solely independent and make correalated errors. The more diverse your weak classifiers the stronger your strong classifier. 

Training Voting Classifier
```python
log_clf = LogisticRegression()
rnd_clf = RandomForestClassifier()
svm_clf = SVC()

voting_clf = VotingClassifier(
	estimators=[('lr', log_clf),('rf', rnd_clf),('svc',svm_clf)],
	voting='hard'							  
)
voting_clf.fit(X_train, y_train)
```

Evaluating Classifiers
```python
for clf in (log_clf, rnd,clf, svm_clf, voting_clf):
	clf.fit(X_train, y_train)
	y_pred = clf.predict(X_test)
	print(clf.__class__.__name__, accuracy_score(y_test, y_pred))
```

Soft-voting is where classes are selected based on individual probabilities and not individual selections. This often outperforms hard-voting due to weights correlating with confidence of guess. 

Previous:
[[Intro]]
Next:
[[Bagging and Pasting]]