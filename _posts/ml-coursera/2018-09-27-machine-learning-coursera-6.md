---
title: ML Coursera 6 - Week 6
categories: [ml, it]
tags: [machine learning, ml coursera]
math: 1
toc: 1
comment: 1
date: 2018-10-04
---

{% assign img-url = '/images/posts/ML/coursera' %}

This note was first taken when I learnt the [machine learning course on Coursera](https://www.coursera.org/learn/machine-learning/).<br />
**Lectures in this week**: [Lecture 10](/files/ML-coursera/Lecture10.pdf).

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

## Bias vs Variance

### Diagnosing bias vs Variance

### Regularization and Bias/Variance

### Learning Curves

### Deciding what to do next revisited

## Building A spam classifier

### Prioritizing what to work on

### Error analysis

## Handling skewed data

### Error Metrics for skewed classes

### Training off precision and recall

## Using large data sets

### Data for machine learning


