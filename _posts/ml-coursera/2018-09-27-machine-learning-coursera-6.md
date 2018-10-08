---
title: ML Coursera 6 - Week 6
categories: [ml, it]
tags: [machine learning, ml coursera]
math: 1
toc: 1
comment: 1
date: 2018-10-08
---

{% assign img-url = '/images/posts/ML/coursera' %}

This note was first taken when I learnt the [machine learning course on Coursera](https://www.coursera.org/learn/machine-learning/).<br />
**Lectures in this week**: [Lecture 10](/files/ML-coursera/Lecture10.pdf), [Lecture 11](/files/ML-coursera/Lecture11.pdf).

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Week 5](/machine-learning-coursera-5).
</span>
</div>


{% include toc.html %}

## Evaluating a Learning Algorithm

{% include download.html content="[Download Lecture 10](/files/ML-coursera/Lecture10.pdf)." %}

### Deciding what to try next

Suppose that we have already apply some algorithm of regression but prediction error is bad. 

- Get more training examples (more $m$)
- Try smaller sets of features (less $x\_i)$
- Try getting additional features (more $x\_i)$
- Try adding polynomial features ($x\_1^2, x\_2^2, x\_1x\_2,\ldots$)
- Try decreasing or increasing $\lambda$


### Evaluating a hypothesis

- If **small number of features**, we can evaluate easily with a plot to check that a hypothesis is overfitting or not. Bigger number of features may be hard to do in that way.
- Split data into: <mark>70%</mark> training cases ($m$) + <mark>30%</mark> test cases ($m_{\text{test}}$).
- The new procedure using these two sets is then:
	- Learn $\Theta$ and minimize $J_{train}(\Theta)$ using training set.
	- Compute the test set error $J_{test}(\Theta)$.
- **Misclassification error** (0/1 Misclassification error)

$$
\begin{align}
\text{err}(h_{\Theta}(x),y) 
&= \begin{cases} 
	1 \text{ if } h_{\Theta}(x)\ge 0.5, y=0 \\
	\quad \text{or if }h_{\Theta}(x)< 0.5, y=1 \\
	0, \text{otherwise}
\end{cases}\\
\text{Test error} &= \frac{1}{m_{test}}\sum_{i=1}^{m_{test}} err(h_{\Theta}(x_{test}^{(i)},y_{test}^{(i)}) 
\end{align}
$$

### Model selection and train/validation/test sets

- **Overfitting example**: error measured on training data ($J\_{train}$) is likely smaller than the actual generation error.

- Try with many degree $d$ of polynomial $h$, we can choose the best $d$ based on the error result.

- An option:

  - **Training set**: 60%
  - **Cross validation set**: 20%
  - **Test set**: 20%

- Training error

  $$
  J_{train} (\theta) = \dfrac{1}{2m}\sum_{i=1}^m(h_{\theta}(x^{(i)})-y^{(i)})^2
  $$

- Cross validation error

  $$
  J_{cv} (\theta) = \dfrac{1}{2m_{cv}}\sum_{i=1}^{m_{cv}}(h_{\theta}(x_{cv}^{(i)})-y_{cv}^{(i)})^2
  $$

- Test error

  $$
  J_{test} (\theta) = \dfrac{1}{2m_{test}}\sum_{i=1}^{m_{test}}(h_{\theta}(x_{test}^{(i)})-y_{test}^{(i)})^2
  $$

- **<mark>Algorithm</mark>**

  - Optimize the parameters in $\Theta$ using the training set for each polynomial degree.
  - Find the polynomial degree d with the least error using the cross validation set.
  - Estimate the generalization error using the test set with $J_{test}(\Theta^{(d)})$, ($d$ = theta from polynomial with lower error);

## Bias vs Variance

![Bias vs Variance]({{img-url}}/bias-variance.png){:.no-border .w-700}

### Diagnosing bias vs Variance

- **Bad prediction**: bias or variance?
- Training error decreases if we increase degree $d$ of the polynomial

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Diagnosing bias and variance]({{img-url}}/diagnosing-bias-variance.png){:.no-border .w-500}
</div>
<div class="col s12 l6" markdown="1">
- **High bias (underfitting)**: $J_{train}, J_{cv}$ high and $J_{cv} \simeq J_{train}$.
- **High variance (overfitting**: $J_{train}$ low and $J_{cv} >> J_{train}$.
</div>
</div>

### Regularization and Bias/Variance

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
See again [Linear regression with regularization](/machine-learning-coursera-3#regularized-linear-regression).
</span>
</div>

![Bias vs Variance regularization]({{img-url}}/bias-variance-regularization.png){:.no-border .w-700}

 In order to choose the model and the regularization term $\lambda$, we need to:

1. Create a list of lambdas (i.e. $\lambda \in \\{ 0,0.01,0.02,0.04,0.08,0.16,0.32,0.64,1.28,2.56,5.12,10.24 \\}$);
2. Create a set of models with different degrees or any other variants.
3. Iterate through the $\lambda$s and for each \lambdaλ go through all the models to learn some $\Theta$.
4. Compute the cross validation error using the learned $\Theta$ (computed with $\lambda$) on the $J_{CV}(\Theta)$ **without** regularization or $\lambda = 0$.
5. Select the best combo that produces the <mark>lowest error on the cross validation set</mark>.
6. Using the best combo $\Theta$ and $\lambda$, apply it on $J_{test}(\Theta)$ to see if it has a good generalization of the problem.

![Bias vs Variance regularization 2]({{img-url}}/bias-variance-regularization-2.png){:.no-border .w-700}

### Learning Curves

- If we add <mark>more training</mark> examples, it <mark>doesn't</mark> mean we will get a better result because it also depends on the degree of polynomial we choose (**high bias - underfitting**).
- In the case of **high variance (overfitting)**. <mark>increase the number of training</mark> examples seem <mark>helps</mark>.

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Learning curve: high bias]({{img-url}}/learning-curve-1.png){:.no-border .w-600}
</div>
<div class="col s12 l6" markdown="1">
![Learning curve: high variance]({{img-url}}/learning-curve-2.png){:.no-border .w-600}
</div>
</div>
### Deciding what to do next (revisited)

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Debugging a learning algorithm]({{img-url}}/debug-learning-algorithm.png){:.no-border .w-600}
</div>
<div class="col s12 l6" markdown="1">
![Neural network and overfitting]({{img-url}}/neural-network-overfitting.png){:.no-border .w-600}
</div>
</div>

## Exercise the programmation



## Building A spam classifier

{% include download.html content="[Download Lecture 11/files/ML-coursera/Lecture11pdf)." %}

### Prioritizing what to work on

### Error analysis

## Handling skewed data

### Error Metrics for skewed classes

### Training off precision and recall

## Using large data sets

### Data for machine learning


