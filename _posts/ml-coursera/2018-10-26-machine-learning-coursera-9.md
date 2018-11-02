---
title: "ML Coursera 9 - Week 9: Anomaly Detection & Recommender Systems"
categories: [ml]
tags: [machine learning, ml coursera]
math: 1
toc: 1
comment: 1
---


{% assign img-url = '/images/posts/ML/coursera' %}

This note was first taken when I learnt the [machine learning course on Coursera](https://www.coursera.org/learn/machine-learning/).<br />
**Lectures in this week**: [Lecture 15](/files/ML-coursera/Lecture15.pdf), [Lecture 16](/files/ML-coursera/Lecture16.pdf).

<p markdown="1" class="thi-warning">
<i class="material-icons mat-icon">error</i>
[This note](/files/ML-coursera/note/) of [Alex Holehouse](http://holehouse.org/) is also very useful (need to be used alongside with my note).
</p>

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Week 8](/machine-learning-coursera-8).
</span>
</div>

{% include toc.html %}

## Density Estimation

### Problem motivation

- Check if _there is an anomalous data-point_ in the data?
- How we do this?
  - Using our training dataset we build a model with $p(x)$ "_What is the probability that example x is normal_?"
  - If $p(x_{test}) < \epsilon$: flag this as an anomaly
  - If $p(x_{test}) \ge \epsilon$: flag this as OK.
  - $\epsilon$ is some **threshold probability** value which we define, depending on how sure we need/want to be
- Application: Fraud detection, Manufacturing (aircraft engine), Monitoring computers in data center,...

### Gaussian distribution (normal distribution)

- $\mu$: mean, average of examples.
- $\sigma^2$: standard deviation squared.
- We can take $m-1$ instead of $m$ for $\sigma^2$. Slightly different mathematical problems, but in practice it makes little difference.

<div class="p-mark">
$$
\begin{align}
P(x\mid \mu ,\sigma^2) &= {\frac{1}{\sqrt {2\pi \sigma ^{2}}}}e^{-{\frac {(x-\mu )^{2}}{2\sigma ^{2}}}}, \\
\mu &= \frac{1}{m}\sum_{i=1}^m x^{(i)}, \\
\sigma^2 &= \frac{1}{m}\sum_{i=1}^m (x^{(i)}-\mu)^2
\end{align}
$$
</div>

![Gaussian distribution]({{img-url}}/gaussian.png){:.w-600}

### Algorithm

## Building an Anomaly Detection System

### Developing and Evaluating an Anomaly Dection System 

### Anomaly Detection vs Supervised Learning

### Choosing what features to use

## Multivariate Gaussian distribution

### Multivariate Gaussian distribution

### Anomaly Detection using the Multivariate Gaussian distribution

## Predicting movie ratings

### Problem formulation

### Content based recommendations

## Collaborative filtering

### Collaborative filtering

### Collaborative filtering algorithm

## Low rank matrix factorization

### Vectorization: low rank matrix factorization

### Implementational detail: mean normalization

## Programming assignment

{% include more.html content="[Go to Week 10](/machine-learning-coursera-10)." %}