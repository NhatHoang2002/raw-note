---
layout: post
title: "ML Coursera 9 - w9: Anomaly Detection & Recommender Systems"
categories: [ml]
tags: [machine learning, ml coursera, coursera]
math: 1
toc: 1
comment: 1
date: 2018-11-03
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

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
<div class="p-mark">
$$
\begin{align}
P(x\mid \mu ,\sigma^2) &= {\frac{1}{\sqrt {2\pi \sigma ^{2}}}}e^{-{\frac {(x-\mu )^{2}}{2\sigma ^{2}}}}, \\
\mu &= \frac{1}{m}\sum_{i=1}^m x^{(i)}, \\
\sigma^2 &= \frac{1}{m}\sum_{i=1}^m (x^{(i)}-\mu)^2
\end{align}
$$
</div>
</div>
<div class="col s12 l6" markdown="1">
![Gaussian distribution]({{img-url}}/gaussian.png){:.w-600}
</div>
</div>


### Algorithm

- [Note of Househole](/files/ML-coursera/note/15_Anomaly_Detection.html)
- Given training set $x^{(i)}\in \mathbb{R}^n$ for $i=1,...,m$.

  ![Anomaly algorithm]({{img-url}}/anomaly-algorithm.png){:.w-700}

- $x_j$ feature! for $j=1,...,n$.
- At each feature, there is m example $x_j^{(i)}$ for $i=1,...,m$. From these m examples, we can find (for each feature $x\_j$) a couple $\mu\_j, \sigma\_j^2$.
- Given a test $x^{(test)}\_{j}$, we can compute 

  $$
  p(x^{(test)}) = \Pi_{j=1}^n p(x^{(test)}_j;\mu_j,\sigma_j^2)
  $$

- The importance is the choice of $\epsilon$.

## Building an Anomaly Detection System

### Developing and Evaluating an Anomaly Dection System 

- [Note of Househole](/files/ML-coursera/note/15_Anomaly_Detection.html)
- To develop an anomaly detection system quickly, would be helpful to <mark>have a way to evaluate your algorithm</mark>
- Sometimes, people use the same data set for Cross Validation set and Test but this is not a good practice and less recommended.

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[See again "Handling skewed data"](/machine-learning-coursera-6#handling-skewed-data).
</span>
</div>

- So far we've been treating anomalous detection with unlabeled data. If you have labeled data allows evaluation:  if you think something iss anomalous you can be sure if it is or not.
- If you have CV set you can see how varying $\epsilon$ effects various evaluation metrics. Then <mark>pick the value of epsilon which maximizes the score on your CV set</mark>
- Evaluate algorithm using cross validation
- Do final algorithm evaluation on the test set

### Anomaly Detection vs Supervised Learning

- If we have labeled data, why we not use a supervised learning algorithm?
- When to use anomaly, when to use supervised?

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Anomaly Detection vs Supervised Learning]({{img-url}}/anomaly-vs-supervised.png){:.w-600}
</div>
<div class="col s12 l6" markdown="1">
![Anomaly Detection vs Supervised Learning 2]({{img-url}}/anomaly-vs-supervised-2.png){:.w-600}
</div>
</div>

### Choosing what features to use

- If our data after plot (`hist`) doesn't look like Gaussian shape, we can "make" it again by change the feature a little bit.

  ![For non gaussian features]({{img-url}}/make-like-gaussian.png){:.w-700}

- Suppose your anomaly detection algorithm is performing poorly and outputs a large value of p(x) for many normal examples and for many anomalous examples in your cross validation dataset. Which of the following changes to your algorithm is most likely to help?
  - Try coming up with more features to distinguish between the normal and the anomalous examples.

## Multivariate Gaussian distribution

### Multivariate Gaussian distribution

Problem: in each single gaussian, it's good with high probability but actually not!

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Multivariate Gaussian]({{img-url}}/multivariate-gaussian.png){:.w-600}
</div>
<div class="col s12 l6" markdown="1">
![Multivariate Gaussian 2]({{img-url}}/multivariate-gaussian-2.png){:.w-600}
</div>
</div>

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Multivariate Gaussian 3]({{img-url}}/multivariate-gaussian-3.png){:.w-600}
</div>
<div class="col s12 l6" markdown="1">
![Multivariate Gaussian 4]({{img-url}}/multivariate-gaussian-4.png){:.w-600}
</div>
</div>

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Multivariate Gaussian 5]({{img-url}}/multivariate-gaussian-5.png){:.w-600}
</div>
<div class="col s12 l6" markdown="1">
![Multivariate Gaussian 6]({{img-url}}/multivariate-gaussian-6.png){:.w-600}
</div>
</div>

### Anomaly Detection using the Multivariate Gaussian distribution

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Anomaly Detection using Multivariate Gaussian]({{img-url}}/multivariate-gaussian-anomaly-1.png){:.w-600}
</div>
<div class="col s12 l6" markdown="1">
![Anomaly Detection using Multivariate Gaussian 2]({{img-url}}/multivariate-gaussian-anomaly-2.png){:.w-600}
</div>
</div>

![Original vs Multivariate]({{img-url}}/original-vs-multivariate.png){:.w-700}

(check Househole's note for more details)

## Predicting movie ratings

- Check [Househole's note](/files/ML-coursera/note/16_Recommender_Systems.html).
- <mark>Recommender Systems: important application of ML.</mark>
  - In academy, it has less attension but in industry, it costs!
- There is not so much a technique, it's a <mark>big idea</mark>.
- Recommender systems do this - try and identify the crucial and relevant features

### Problem formulation

There are some movies that some users haven't seen yet. Based on what they have already seen or others did, we can predict their rate for movies that they haven't watched. From these prediction, we can recommend the movies they like (if the predicted rating is high).

### Content based recommendations

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Movie ratings]({{img-url}}/movie-rating.png){:.w-600}
</div>
<div class="col s12 l6" markdown="1">
![Movie ratings 2]({{img-url}}/movie-rating-2.png){:.w-600}
</div>
</div>

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Movie ratings]({{img-url}}/movie-rating-3.png){:.w-600}
</div>
<div class="col s12 l6" markdown="1">
![Movie ratings 2]({{img-url}}/movie-rating-4.png){:.w-600}
</div>
</div>

- This approach is called content-based approach because we assume we have features regarding the content which will help us identify things that make them appealing to a user.
  - However, often such features are not available - next we discuss a non-contents based approach!


## Collaborative filtering

### Collaborative filtering

- It can learn for itself what features it needs to learn.
- The values of $\Theta$ show the "idea" of the user. For example, Alice says that she really like the romantic movie and she doesn't like action movies, i.e. $\Theta = [0 5 0]$.

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Collaborative filtering]({{img-url}}/collaborative-filtering-1.png){:.w-600}
</div>
<div class="col s12 l6" markdown="1">
![Collaborative filtering]({{img-url}}/collaborative-filtering-2.png){:.w-600}
</div>
</div>

### Collaborative filtering algorithm

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Collaborative filtering 3]({{img-url}}/collaborative-filtering-3.png){:.w-600}
</div>
<div class="col s12 l6" markdown="1">
![Collaborative filtering 4]({{img-url}}/collaborative-filtering-4.png){:.w-600}
</div>
</div>

## Low rank matrix factorization

### Vectorization: low rank matrix factorization

- Having looked at collaborative filtering algorithm, how can we improve this? Given one product, can we determine other relevant products?

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Low rank matrix factorization 1]({{img-url}}/low-rank-matrix-1.png){:.w-600}
</div>
<div class="col s12 l6" markdown="1">
![Low rank matrix factorization 2]({{img-url}}/low-rank-matrix-2.png){:.w-600}
</div>
</div>

### Implementational detail: mean normalization

![Mean normalization]({{img-url}}/mean-nomallization.png){:.w-700}

- We don't scale the value because all movies have alreay been scale by rates.
