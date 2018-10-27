---
title: "ML Coursera 8 - Week 8: Unsupervised Learning"
categories: [ml, it]
tags: [machine learning, ml coursera]
math: 1
toc: 1
comment: 1
date: 2018-10-27
---


{% assign img-url = '/images/posts/ML/coursera' %}

This note was first taken when I learnt the [machine learning course on Coursera](https://www.coursera.org/learn/machine-learning/).<br />
**Lectures in this week**: [Lecture 13](/files/ML-coursera/Lecture13.pdf), [Lecture 14](/files/ML-coursera/Lecture14.pdf).

<p markdown="1" class="thi-warning">
<i class="material-icons mat-icon">error</i>
[This note](/files/ML-coursera/note/) of [Alex Holehouse](http://holehouse.org/) is also very useful (need to be used alongside with my note).
</p>

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Week 7](/machine-learning-coursera-7).
</span>
</div>


{% include toc.html %}

## Clustering

### Unsupervised Learning

- This is the first unsupervised learnig.
- There is no label associated to it.
- There is X but not y.
- Unsupervised learning
	- Try and determining structure in the data
	- Clustering algorithm groups data together based on data features

## K-means Algorithm

- The <mark>most popular</mark> and widely used algorithm.
- See here for the [figure of idea](/files/ML-coursera/note/13_Clustering.html)
- <mark>Algorithm</mark>: **Cluster assignment step** and **Move centroid step**

	![Clustering algorithm 1]({{img-url}}/clustering-1.png){:.w-700}

### Optimization objective

- K-means also have an optimization objective (cost function like supervised learning)
- Knowing this is helpful because
	- Help for debugging
	- Help find better clustering
- **distortion cost function**

	![Distortion cost function 1]({{img-url}}/distortion-1.png){:.w-700}

- Minimize to find out the $c^{(i)}$ and $\mu_{c^{(i)}}$

	![Clustering algorithm 2]({{img-url}}/clustering-2.png){:.w-700}

### Random Initialization

- Also talk about how to avoid **local optimal** as well.
- $K$: number of clusters, $m$: the number of training examples (usually $K<m$)
- <mark>Random choose $K$ training examples as a initial cluster.</mark>
	- If we choose the wrong examples, it may lead to **a local optima**
	- To avoid that, dun random K-means multiple times (100 times, for example)
		- Give 100 diff ways to K
		- Choose the one make $J$ min
		- <mark>Only apply when $K=2,...,10$</mark>

### Choosing the number of clusters

- **Elbow method**: check the cost function J wrt number of clusters.
	- Check the "elbow" (cái cùi chỏ) where the graph change direction much.
	- EM <mark>isn't</mark> used very often!

	![Elbow method 1]({{img-url}}/elbow-1.png){:.w-600}

- If $k=5$ have bigger J than $k=3$ then k-means got stuck in a bad local minimum. You should try re-running k-means with multiple random initializations.
- Choose the number of clusters depend on **later/downstream purpose** (choose the size of T-shirt, 3 or 5 for example).

## Dimensionality reduction

- **Motivation**: data compression + data visualization
- [Househole's note](/files/ML-coursera/note/14_Dimensionality_Reduction.html).

### Data compression

- Speeds up algorithms + Reduces space used by data for them.
	- If all points in 2D lay on 1 straight line, we can reduce them to 1D cases. The same for 3D to 2D

![Data compression]({{img-url}}/data-compression.png){:.w-700}

### Data Visualization

- We want to reduce dimension to 2 or 3 so that we can visualize the data.

## Principal component analysis (PCA)

### PCA formulation

- [Househole's note](/files/ML-coursera/note/14_Dimensionality_Reduction.html).
- For the problem of dimensionality reduction the <mark>most commonly used</mark> algorithm is PCA
- For example, we want to find a line to translate 2D to 1D: all **data point projected to this line** should be small. The vector of this line is what we wanna find.
- You should normally do **mean normalization** and **feature scaling** ([see again](/machine-learning-coursera-2#gd-in-practice--feature-scaling)) on your data before PCA
- <mark>PCA is not linear regression!!</mark>: PCA lấy error là các projection trong khi LG lấy error là sự sai lệch (theo y)
	- Below photo comapre pca (right) and linear regression (left).
	- LR has y to compare while PCA has no y, every x has equal role.

	![PCA vs LR]({{img-url}}/pca-1.png){:.w-600}

### PCA algorithm

- How to use PCA for yourself + and how to reduce dimension for your data.
- Data preprocessing: [feature scaling/mean normalization](/machine-learning-coursera-2#gd-in-practice--feature-scaling)
- `svd` in matlab/octave = "**singular value decomposition**" or `eig` function with the same function (`svd ` is more numerically stable than eig)

	![PCA algorithm]({{img-url}}/pca-2.png){:.w-700}

	- After having U, just take first k column if we wanna k dimension from n

	![PCA algorithm]({{img-url}}/pca-3.png){:.w-700}

- **Algorithm**:

	![PCA algorithm]({{img-url}}/pca-4.png){:.w-700}


## Applying PCA

### Reconstruction from compressed representation

**From z back to x**: 2D back to 1D for example,

![PCA Reconstruction]({{img-url}}/pca-5.png){:.w-700}

### Choosing the number of principal components

![PCA choosing k]({{img-url}}/pca-choose-k.png){:.w-700}

Choo k from 1 to the one get the fraction less than 0.001.

![PCA choosing k]({{img-url}}/pca-choose-k-2.png){:.w-700}

**The numerator is small**: we lose very little information in the dimensionality reduction, so when we decompress we regenerate the same data.

### Advice for applying PCA

- Andrew uses PCA very often
- Defined by PCA <mark>only on the training set</mark>
	- And then use those obtained parameters to the Cross validation data and test set
- A <mark>bad use of PCA</mark>: Use it to prevent over-fitting --> Better to **use regularization**
- Always use normal approach (without PCA) to solve a problem, if you CANNOT DO MORE, then think about adding PCA.

## Programming assignment


{% include more.html content="[Go to Week 9](/machine-learning-coursera-9)." %}



