---
title: ML Coursera 5 - Week 5
categories: [ml, it]
tags: [machine learning, ml coursera]
math: 1
toc: 1
comment: 1
date: 2018-09-21
---

{% assign img-url = '/images/posts/ML/coursera' %}

This note was first taken when I learnt the [machine learning course on Coursera](https://www.coursera.org/learn/machine-learning/).<br />
**Lectures in this week**: [Lecture 9](/files/ML-coursera/Lecture9.pdf).

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Week 4](/machine-learning-coursera-4).
</span>
</div>


{% include toc.html %}

## Cost function & Backpropagation

### Cost function

**Notations**

- <mark>$L$</mark> = total number of layers in network
- <mark>$s_l$</mark> = no. of units (not counting bias unit) in layer $l\in L$

**Recall**

- **Binary classification** ([review](/machine-learning-coursera-3#classification)) : 
	- $y\in \{0,1\}$, <mark>1 output unit</mark>
	- $h_{\Theta}(x)\in \mathbb{R}$
	- $s_L = 1$ (1 output unit)
	- $K=1$ ($K$ = no. of units in the output layer)
- **Multi-class classification** with $K$ classes ([review](/machine-learning-coursera-3#multiclass-classification-one-vs-all)): $y\in \mathbb{R}^K$ and <mark>K output units</mark>
	- $h_{\theta}(x) \in \mathbb{R}^K$
	- $s_L = K$ (<mark>$K\ge 3$</mark>) because if $K=2$, we can use binary classification.

**Cost function**

- **Logistic regression** (review [here](/machine-learning-coursera-3#cost-function) and [here](Regularized logistic regression)):

	<div class="p-mark">
	$$
	J(\theta) = - \frac{1}{m} \displaystyle \sum_{i=1}^m [y^{(i)}\log (h_\theta (x^{(i)})) + (1 - y^{(i)})\log (1 - h_\theta(x^{(i)}))]
	+
	\dfrac{\lambda}{2m}\sum_{j=1}^n \theta_j^2.
	$$
	</div>

- **Neural network** ([review](/machine-learning-coursera-4#neural-networks))

	<div class="p-mark">
	$$
	J(\Theta) = - \frac{1}{m} \sum_{i=1}^m \sum_{k=1}^K \left[y^{(i)}_k \log ((h_\Theta (x^{(i)}))_k) + (1 - y^{(i)}_k)\log (1 - (h_\Theta(x^{(i)}))_k)\right] + \frac{\lambda}{2m}\sum_{l=1}^{L-1} \sum_{i=1}^{s_l} \sum_{j=1}^{s_{l+1}} ( \Theta_{j,i}^{(l)})^2
	$$
	</div>

	- If we want to minimize $J(\Theta)$ as a function of $\Theta$ using one of the advanced optimization methods (fminunc, conjugate gradients, BGGS, L-BFGS, ...) we need to supply $J(\Theta)$ and the (partial) gradient derivative terms $\frac{\partial}{\partial \Theta_{ij}^{(l)}}$ for every $i,j,l$.
	- The triple sum simply adds up the squares of all the individual $\Theta$s in the entire network.
	- The $i$ in the triple sum **does not** refer to training example $i$.


### <mark>Backpropagation algorithm</mark>




### Cost function

### Backpropagation algorithm

### Backpropagation intuition





## Backpropagation in practice

### Implementation note: Unrolling parameters

### Gradient checking

### Randon initialization

### Putting it together



## Application of Neural networks





## Exercise de programmation: Neural network learning








