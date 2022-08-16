# Clustering
## K-means
1. Cluster Assignment
2. Centroid step

### Cluster Assignment
Each point is grouped with closest centroid

### Centroid Step
Assign each centroid to the center of its cluster

### K?
One input into this algorithm is the value of k which is how many clusters there are. 

## Algorithm
Randomly intialize Centroids
$\mu_1, \mu_2,\cdots,\mu_k\hspace{0.25em}\epsilon\mathbb{R}^n$
repeat {
	for i = 1 to m
		$c^{(i)} := \text{ index}$(from 1 to K) of cluster centroids
			closest to $x^{(i)}$
	for k = 1 to K
		$\mu_k :=$ mean of points in cluster k
}

Here $c^{(i)}$ is the cluster index

## Optimization Objective
$$\underset{\mu_1,\cdots,\mu_k}{\underset{c^{(1)},\cdots,c^{(m)}}{min}}=\frac{1}{m}\sum^m_{i=1}||x^{(i)}-\mu_{c^{(i)}}||^2$$
## Random Initialization
Have K < m
randomly pick k training examples and set these to the centroids as well
To escape local optima run k-means multiple times

## Choosing K
Use the elbow method to find ideal, although often it's generally better to pick k based off of a downstream purpose

