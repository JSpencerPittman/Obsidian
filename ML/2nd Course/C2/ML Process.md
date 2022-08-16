## Iterative loop of ML Development
Choose Architecture (model, data, etc.) 
	$\LARGE\downarrow$
Train Model
	$\LARGE\downarrow$
Diagnostics (bias, variance, and error analysis)
	$\LARGE\downarrow$
Repeat

## Error Analysis
Why are your errors wrong?
Patterns?

## Data Augmentation
Rather than just adding more data for the heck of it, attempt to get data that error analysis has indicated a need for more training in specific areas.

Dont add purely random/meaningless noise to your data
Representative of the type of noise/distortions in the test set

## Transfer Learning
Take previosuly trained neural network for another task and use it for ours in two possible ways

1. Train output parameters
	- Better for smaller training sets
2. Train all parameters
	- Better for larger training sets

**Supervised Pretraining**: Train on a large dataset for unrelated task
**Fine Tuning**: Retrain for your task

Allows us to outsource supervised pretraining to others and merely fine tune it to your own designated task.

## Full cycle of a project
1. Scope/Define Project
	- What is the project? 
	- What are you doing?
2. Collect Data
	- Define and collect data
	- What type do you need?
3. Train Model
	- Training, error analysis, iterative improvement
	- If need be go back to the collect data stage
4. Deploy in production
	- Deploy, monitor and maintain system
	- If performance is slacking go back to train model or collect data
	- Or collect data activley from others using your project

### Deployment
A common way to deploy a ML project is to put your machine learning model implemented in a server called an "inference server". 

Software engineering may be needed for:
	Reliable and efficent predictions while keeping cost down
	Scaling
	Logging
	System Monitoring
	Model updates


MLOps - Machine Learning Operations
	handles a lot of this

## Systems that interact with people
If your ML system affects people, make sure it's ethical and fair. 

The key to limit bias:
	A diverse team to brainstorm things that might go wrong, with emphasis on possible harm to vulnerable groups. Diversity should be all possible factors: race, gender, class, education.
	Literature search on standards/guidlines for your industry.
	Audist systems against possible harm prior to deployment. If applicable try to do it before the deployment stage.
	Develop a mitigation plan (if applicable), and after deployment monitor for possible harm.