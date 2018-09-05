---
title: ML Coursera 3 - Week 3
categories: [ml, it]
tags: [machine learning, ml coursera]
math: 1
toc: 1
comment: 1
date: 2018-09-04
---

{% assign img-url = '/images/posts/ML/coursera' %}

This note was first taken when I learnt the [machine learning course on Coursera](https://www.coursera.org/learn/machine-learning/).<br />
**Lectures in this week**: [Lecture 4](/files/ML-coursera/Lecture4.pdf).

{% include more.html content="[Go back to Week 2](/machine-learning-coursera-2)." %}

{% include toc.html %}

## Classification & Representation

### Classification

- Variable $y$ has discrete values.

- Other name of :  1 (positive class), 0 (negative class) $\Rightarrow$ **binary classification problem**

- If y has more than 2 values, it's called **multi classification**

- Using linear regression in this case seems not to be very good because there may be some values that effects much more than the others (blue line).

  ![Classification 1]({{img-url}}/classification-1.png){:.no-border .w-600}

- $h_{\theta}$ may take values >1 or <0 but <mark>we want $0\le h_{\theta} \le 1$</mark>. That's why we need **logistic regression**, i.e. $h_{\theta}$ is always between $[0,1]$

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

Look back to the [cost function in linear regression](/machine-learning-coursera-1#cost-function).

$$
\begin{align}
J(\theta) &= \dfrac{1}{m}\sum_{i=1}^m \text{Cost}(h_{\theta}(x^{(i)}),y^{(i)}), \\
\text{Cost}(h_{\theta}(x),y) &= 
  \begin{cases}
    -\log(h_{\theta}(x)) \quad \text{ if } y=1, \\
    -\log(1-h_{\theta}(x)) \quad \text{ if } y=0.
  \end{cases}
\end{align}
$$

or we can write,

<div class="p-mark">
$$
\text{Cost}(h_{\theta}(x),y) = -y \log(h_{\theta}(x),y) - (1-y)\log(1-h_{\theta}(x),y)
$$
</div>

**The cost function** is rewritten as

<div class="p-mark">
$$
J(\theta) = - \frac{1}{m} \displaystyle \sum_{i=1}^m [y^{(i)}\log (h_\theta (x^{(i)})) + (1 - y^{(i)})\log (1 - h_\theta(x^{(i)}))]
$$
</div>

**Vectorization**

<div class="p-mark">
$$
\begin{align*} 
h &= g(X\theta) \\ 
J(\theta) &= \frac{1}{m} \cdot \left(-y^{T}\log(h)-(1-y)^{T}\log(1-h)\right) 
\end{align*}
$$
</div>

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Cost function of logistic regression 1]({{img-url}}/cost-function-logistic-1.png){:.no-border}
</div>
<div class="col s12 l6" markdown="1">
![Cost function of logistic regression 1]({{img-url}}/cost-function-logistic-2.png){:.no-border}
</div>
</div>

$$
\begin{align*}
\mathrm{Cost}(h_\theta(x),y) &= 0 \text{ if } h_\theta(x) = y \\
\mathrm{Cost}(h_\theta(x),y) &\rightarrow \infty \text{ if } y = 0 \; \mathrm{and} \; h_\theta(x) \rightarrow 1 \\
\mathrm{Cost}(h_\theta(x),y) &\rightarrow \infty \text{ if } y = 1 \; \mathrm{and} \; h_\theta(x) \rightarrow 0 
\end{align*}
$$


<div class="p-mark" markdown="1">
- If hypothesis seems to be "wrong" ($h \to 1$ while $y\to 0$ or $h \to 0$ while $y\to 1$) then $\text{Cost}\to \infty$
- $J(\theta)$ ins this style is <mark>always convex</mark>.
</div>

### Simplified Cost Function and Gradient Descent

Review the gradient decent in linear regression [here](/machine-learning-coursera-1#gradient-descent).

In this logistic regression,

<div class="p-mark">
Repeat{
$$
\begin{align*} 
\theta_j := \theta_j - \frac{\alpha}{m} \sum_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)}) x_j^{(i)}
\end{align*}
$$
(Simutanously update all $\theta_j$)
}
</div>

Notice that, above equation looks the same with one in linear regression, <mark>the different is def of $h_{\theta}$!</mark>

**Vectorization**

<div class="p-mark">
$$
\theta := \theta -\frac{\alpha}{m} X^T(g(X\theta)-y)
$$
</div>

### Advanced Optimization

## Multiclass classification: one-vs-all
