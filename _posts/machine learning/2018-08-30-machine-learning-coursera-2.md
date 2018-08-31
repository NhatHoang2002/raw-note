---
title: ML Coursera 2 - Week 2
categories: [ml, it]
tags: [machine learning, ml coursera]
math: 1
toc: 1
date: 2018-09-01
---

{% assign img-url = '/images/posts/ML/coursera' %}

This note was fist taken when I learnt the [machine learning course on Coursera](https://www.coursera.org/learn/machine-learning/).

{% include more.html content="[Go back to Week 1](/machine-learning-coursera-1)." %}

{% include toc.html %}

## Multivariate Linear Regression

{% include more.html content="[Download Lecture 4](/files/ML-coursera/Lecture4.pdf)." %}

### Multiple Features

Linear regression with multiple variables is also known as "**multivariate linear regression**". We now introduce notation for equations where we can have any number of input variables.

- $x^{(i)}\_j$ = value of feature j in the ith training example
- $x^(i)$ = the input (features) of the ith training example
- m = the number of training examples
- n = the number of features

The multivariable form of the hypothesis function accommodating these multiple features is as follows:

$$h_\theta (x) = \theta_0 + \theta_1 x_1 + \theta_2 x_2 + \theta_3 x_3 + \cdots + \theta_n x_n$$ 

In order to develop intuition about this function, we can think about $\theta_0$ as the basic price of a house, $\theta_1$ as the price per square meter, $\theta_2$ as the price per floor, etc. $x_1$ will be the number of square meters in the house, $x_2$ the number of floors, etc.

Using the definition of matrix multiplication, our multivariable hypothesis function can be concisely represented as:

$$
h_{\theta}(x) = [\theta_0 \theta_1 \ldots \theta_n] 
	\left[\begin{matrix} x_0 \\ x_1 \\ . \\ . \\ x_n \end{matrix}\right]
    = \theta^T x.
$$

This is a vectorization of our hypothesis function for one training example; see the lessons on vectorization to learn more.

Remark: Note that **for convenience** reasons in this course <mark>we assume $x_{0}^{(i)} =1 \text{ for } (i\in { 1,\dots, m } )$</mark>. This allows us to do matrix operations with theta and x. Hence making the two vectors $\theta$ and $x^{(i)}$ match each other element-wise (that is, have the same number of elements: n+1).

### Gradient descent for multiple variables

The gradient descent equation itself is generally the same form; we just have to repeat it for our 'n' features:

<div class="p-mark">
Repeat until convergence: {
$$
\begin{align}
    \theta_0 &:= \theta_0 - \alpha \frac{1}{m}\sum_{i=1}^m (h_{\theta}(x^{(i)}-y^{(i)}))\cdot x_0^{(i)} \\
    \theta_1 &:= \theta_1 - \alpha \frac{1}{m}\sum_{i=1}^m (h_{\theta}(x^{(i)}-y^{(i)}))\cdot x_1^{(i)} \\
    \ldots
\end{align}
$$
}
</div>
In other words:

<div class="p-mark">
Repeat until convergence: {
$$
\theta_j := \theta_1 - \alpha \frac{1}{m}\sum_{i=1}^m (h_{\theta}(x^{(i)}-y^{(i)}))\cdot x_j^{(i)}, \quad \text{for }j=1,\ldots,n.
$$
}
</div>

The following image compares gradient descent with one variable to gradient descent with multiple variables:

![Gradient descent for multiple variables 1]({{img-url}}/gd-mv-1.png){:.no-border}

### GD in practice : Feature scaling

<div class="p-mark">
Make sure feature are on similar scale!
</div>

- If features have diff values, when we perform them on a plot, there may be very different on scale between axes! <mark>It may impact on the gradient descent!</mark>
- An option is to divide to a maximum value, for example, $x \in \\{1,\ldots, 2000\\}$ can be scale to $\bar{x} \in \dfrac{\\{1,\ldots,2000\\}}{2000}$ so that we have the values are between $[-1,1]$. However, not used for range of $[-100,100]$ of bigger or $[-0.0001,0.0001]$ or smaller.
- Another option is to use **mean normalisation**

    $$
    \bar{x}_i = \dfrac{x_i - \mu_i}{\text{range of }x_i}, \quad
    \mu_i = \Sigma_i \frac{x_i}{n}.
    $$
    
    For example, $x\_i \in [30,50]$, then range of $x\_i$ is 20.


### GD in practice : Learning rate $\alpha$

$$
\theta_j = \theta_j - \alpha \dfrac{\partial}{\partial \theta_j} J(\theta)
$$

- **Debugging**: How to make sure gradient descent works correctly?
- How to choose **learning rate** $\alpha$?

Methods

- Examine the convergence of $\min_{\theta} J(\theta)$ w.r.t the number of iterations.
- Declare convergence if $J(\theta)$ decreases by <mark>less than $10^{-1}$</mark> in one iteration.

	![Multivariate Linear Regression 1]({{img-url}}/multivartiate-linear-regression-1.png){:.no-border}

- If $J(\theta)$ increase, use smaller $\alpha$ (can prove it mathematically).
- But if $\alpha$ is too small, gradient descent can be slow to converge.
- Try $\alpha$ with $0.001, 0.003, 0.01, 0.03, 0.1, 0.3, 1,\ldots $ (try a little bit and get the good value of $\alpha$)

	![Multivariate Linear Regression 2]({{img-url}}/multivartiate-linear-regression-2.png){:.no-border}

### Features and Polynomial Regression

We can improve our features and the form of our hypothesis function in a couple different ways. We can combine multiple features into one. For example, we can combine $x_1,x_2$ into a new feature called $x_3 = x_1x_2$.

We can **change the behavior or curve** of our hypothesis function by making it a quadratic, cubic or square root function (or any other form).

For example, if our hypothesis function is $h_\theta(x) = \theta_0 + \theta_1 x_1$ then we can create additional features based on $x_1$ to get the quadratic function $h_\theta(x) = \theta_0 + \theta_1 x_1 + \theta_2 x_1^2$ or the cubic function $h_\theta(x) = \theta_0 + \theta_1 x_1 + \theta_2 x_1^2 + \theta_3 x_1^3$

In the cubic version, we have created new features $x_2$ amd $x_3$ where $x_2=x_1^2, x_3=x_1^3$
​	 .
To make it a square root function, we could do: $h_\theta(x) = \theta_0 + \theta_1 x_1 + \theta_2 \sqrt{x_1}$

One important thing to **keep in mind** is, <mark>if you choose your features this way then feature scaling becomes very important.</mark>

For example, if $x_1$ has range 1-10, then $x_1^2$ has range 1-100, $x_1^3$ has range 1-1000.

## Computing Parameters Analytically

### Normal equation

- **Normal equation**: method to solve for $\theta$ analytically (instead of solve it by iteration)
- Example, **m examples**, **n feautures** then the **design matrix** X will be

	$$
	m \times (n+1)
	$$

	The first column is the supposed feature whose all values are equal to 1.
- the value of <mark>$\theta$ that minimize your cost function $J(\theta)$ </mark>

	$$
	\theta = (X^TX)^{-1}X^Ty
	$$
 
	![Example of normal equation]({{img-url}}/normal-equation-1.png){:.no-border}

- In this case (**normal equation**, analytically), <mark>feature scaling seem snot to be important!</mark>
- But in **gradient descent**, feature scaling is important!
- If <mark>number of features is less than 10000, use normal equation.</mark>. If bigger than that, change to iterative process.

|--------------------------------+-------------------------------------------------|
| **Gradient Descent**           | **Normal Equation**                             |
|--------------------------------|-------------------------------------------------|
| Need to choose alpha           | No need to choose alpha                         |
| Needs many iterations          | No need to iterate                              |
| $O(kn^2)$                      | $O (n^3)$, need to calculate inverse of $X^TX$  |
| Works well when n is large     | Slow if n is very large                         |


### Normal equation noninvertibility

