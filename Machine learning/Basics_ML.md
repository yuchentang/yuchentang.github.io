---
sort: 1
---

# Some Basics of Machine Learning

## What is Machine Learning?

> [Machine Learning is the] field of study that gives computers the ability to learn without being explicitly programmed.
> 
> -- Arthur Samuel, 1959


> A computer program is said to learn from experience E with respect to some task T and some performance measure P, if its performance on T, as measured by P, improves with experience E.
> 
> -- Tom Mitchell, 1997

E.g. An email spam filter. 

- The task T: to flag spam for new emails
- The experience E: the training data
- The performance measure P: needs to be defined; E.g. the ratio of correctly classified emails (accuracy)

## Categories of Machine Learning

Four major categories:

- Supervised learning
   - k-Nearest Neighbors (KNN)
   - Linear Regression
   - Logistic Regression
   - Support Vector Machines (SVM)
   - Decision Trees and Random Forests
   - Neural networks [^1]

[^1]: Some neural network architectures can be unsupervised, such as autoencoders and restricted Boltzmann machines. They can also be semisupervised, such as in deep belief networks and unsupervised pretraining.
   
- Unsupervised learning
	- Clustering 
		- K-Means 
		- DBSCAN 
		- Hierarchical Cluster Analysis (HCA)
	- Anomaly detection and novelty detection
		- One-class SVM
		- Isolation Forest
	- Visualization and dimensionality reduction
		- Principal Component Analysis (PCA)
		- Kernel PCA
		- Locally Linear Embedding (LLE)
		- t-Distributed Stochastic Neighbor Embedding (t-SNE)
	- Association rule learning
		- Apriori
		- Eclat

- Semisupervised learning
- Reinforcement Learning

Another criterion: whether or not be incapable of learning incrementally.

- Batch learning
- Online learning

## THE Unreasoballe Effectiveness of Data

Michele Banko and Eric Brill (2001) : Very different Machine Learning algorithms, including fairly simple ones, performed almost identically well on a complex problem of natural language disambiguation 8 once they were given enough data.

<img src="https://github.com/yuchentang/yuchentang.github.io/blob/main/assets/images/banko_2001.png?raw=true" alt="banko_2001" width="500"/>

## No Free Lunch Theorem (NFL)

All optimization algorithms perform equally well when their performance is averaged across all possible problems.