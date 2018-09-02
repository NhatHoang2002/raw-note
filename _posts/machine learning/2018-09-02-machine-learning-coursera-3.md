---
title: ML Coursera 3 - Week 3
categories: [ml, it]
tags: [machine learning, ml coursera]
math: 1
toc: 1
comment: 1
date: 2018-09-02
---

{% assign img-url = '/images/posts/ML/coursera' %}

This note was first taken when I learnt the [machine learning course on Coursera](https://www.coursera.org/learn/machine-learning/). Lectures in this week: [Lecture 4](/files/ML-coursera/Lecture4.pdf).

{% include more.html content="[Go back to Week 2](/machine-learning-coursera-2)." %}

{% include toc.html %}

## Classification & Representation

### Classification

- Variable $y$ has discrete values.

- Other name of :  1 (positive class), 0 (negative class) $\Rightarrow$ **binary classification problem**

- If y has more than 2 values, it's called **multi classification**

- Using linear regression in this case seems not to be very good because there may be some values that effects much more than the others (blue line).

  ![Classification 1]({{img-url}}/classification-1.png){:.no-border .w-600}

- $h_{\theta}$ may take values >1 or <0 but we want <mark>$0\le h_{\theta} \le 1$</mark>. That's why we need **logistic regression**, i.e. $h_{\theta}$ is always between $[0,1]$

- Remember and not confused that *logistic regression* is just a *classification regression* in cases of y taking discrete values.

### Hypothesis representation

- What is the function we are going to use to *represent* the *hypothesis*

- **Logistic regression**

<div class="p-mark">
  $$
  \begin{align}
  h_{\theta}(x) &= g(\theta^Tx) \\
  g(z) &= \dfrac{1}{1+e^{-z}}, \\
  h_{\theta} &= \dfrac{1}{e^{-\theta^Tx}}
  \end{align}
  $$
</div>

- They are the same: **<mark>sigmoid function = logistic function = $g(z)$</mark>**

![Logistic function g(z)]({{img-url}}/classification-2.png){:.no-border .w-800}

- Some propabilities


$$
\begin{align*}& h_\theta(x) = P(y=1 | x ; \theta) = 1 - P(y=0 | x ; \theta) \newline& P(y = 0 | x;\theta) + P(y = 1 | x ; \theta) = 1\end{align*}
$$



### Decision Boundary

From the above figure, we see that


$$
\begin{align*}& h_\theta(x) \geq 0.5 \rightarrow y = 1 \newline& h_\theta(x) < 0.5 \rightarrow y = 0 \newline\end{align*}
$$


We have

<div class="p-mark">

$$
\begin{align*}& \theta^T x \geq 0 \Rightarrow y = 1 \newline& \theta^T x < 0 \Rightarrow y = 0 \newline\end{align*}
$$

</div>

The **decision boundary** is the <mark>line that separates the area where y = 0 and where y = 1</mark>mark>. It is created by our hypothesis function. 

An example,

![Example of decision boundary]({{img-url}}/classification-3.png){:.no-border .w-800}

The training set is not used to determine the decision boundary, but parameter $\theta$. <mark>The training set is used only for fit the parameter $\theta$.</mark>

![Example of decision boundary]({{img-url}}/classification-4.png){:.no-border .w-800}

## Logistic regression model

### Cost function

### Simplified Cost Function and Gradient Descent

### Advanced Optimization

## Multiclass classification: one-vs-all