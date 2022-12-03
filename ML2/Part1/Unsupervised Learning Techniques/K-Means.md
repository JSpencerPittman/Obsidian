# K-Means
### Uses
Customer Segmentation:
	Cluster customers based on purchases and activity
	Very useful in recommender systems
Data Analysis
	Analyze a new dataset and analyze each identified cluster
Dimensionality Reduction Technique
	Measure each instances affinity for a cluster
	k clusters k-dimensionsal dataset
Anomaly Detection
	Low affinity to all clusters is a signal of an anomaly
Semi-supervised learning
	Labels the dataset automatically for a supervised learning algorithm to train on
Search Engines
	Return similar results (same cluster)
Segment an image
	Clustering pixels according to color
	Reduce colors in an image

Some look for instances centered around a so called *centroid* while others look for continous regressions
of densely packed instances

## K-Means
Try's to find the center of each cluster and the assign each instance to the closest blob
Doesn't behave well when blobs have different diameters

**Hard Clustering**
Assign each instance to a single cluster

**Soft Clustering**
Give each instance a a score per cluster
Score can be distance from centroid, or similarity score

#### K-Means Algorithm
Start by placing $k$ random centroids
Then labels the instances and update the centroids and so on so forth
Until the centroids converge which is guaranteed to be in a finite number of steps. 

If the data has a clustering stucture run time is often $O(mnk)$
However if it doesn't have a clustering structure then complexity can be exponential, although this is quite rare

Algorithm does get stuck on local optima
To minimize this look below

#### Centroid Initialization Methods
If you have an idea of where centroids should be then can you set an init hyperparameter
Or run multiple times with different random inits and keep the best one

Which solutions best?
The performance metric of the model's inertia finds this for us. The Inertia is the mean squared distance between each instance and its closest centroid. Keeps model with the lowest inertia. 

K-Means++ uses a smarter intialization step was to initialize centroids an equal distance from each other.
1. Take one centroid $c^{(i)}$ that's chosen uniformly at random from the dataset
2. Choose a new $c^{(i)}$, choosing an instance $x^{(i)}$ with probability $D(x^{(i)})^2/\sum^m_{j=1}D(x^{(j)})^2$ where $D(x^{(i)})$ is the distance between $x^{(i)}$ and the closest centroid. Father instances more likely to be chosen.
3. Repeat steps 1-2 until k centroids are found

#### Accelerated K-means and mini-batch K-means
Avoids many unecessary distance calculations
using the triangle inequality and keeping track of lower and upper bounds for distances between instances and centroids

Also instead of using the full dataset at each iteration we can use mini-batches moving the centroids slightly for each batch and makes clustering of large datasets feasible. Although mini-batch does have a worser inertia function.

#### Finding the optimal number of clusters
Can't use inertia because as clusters rise interia goes down regardless of whether its optimal $k$
We can identify an elbow in the curve or use a *silhouette score* which is mean *silhouette coefficent* over all instances. A silhouette coefficent is $(b-a)/max(a,b)$ where a is the mean distance to other instances in said cluster and b is the mean nearest-cluster distance. b is the instances of the next closes cluster. +1 is good, -1 is awful and 0 is cluster boundary. The more similar the shiloette scores of each cluster the better.

## Limits of K-Means
Multiple runs, specify number of clusters, can't handle very well varying sizes, densities, or nonspherical shapes
Also scaling the input features is very important. 

previous:
[[Part1/Unsupervised Learning Techniques/Introduction]]
next:
