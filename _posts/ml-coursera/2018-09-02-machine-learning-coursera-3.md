---
title: "ML Coursera 3 - Week 3: Logistic Regression"
categories: [ml, it]
tags: [machine learning, ml coursera]
math: 1
toc: 1
comment: 1
date: 2018-09-11
---

{% assign img-url = '/images/posts/ML/coursera' %}

This note was first taken when I learnt the [machine learning course on Coursera](https://www.coursera.org/learn/machine-learning/).<br />
**Lectures in this week**: [Lecture 6](/files/ML-coursera/Lecture6.pdf), [Lecture 7](/files/ML-coursera/Lecture7.pdf).

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Week 2](/machine-learning-coursera-2).
</span>
</div>

{% include toc.html %}

## Classification & Representation

{% include download.html content="[Download Lecture 6](/files/ML-coursera/Lecture6.pdf)." %}

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

	<div class="p-mark">
	$$
	\begin{align*}& h_\theta(x) = P(y=1 | x ; \theta) = 1 - P(y=0 | x ; \theta) \newline& P(y = 0 | x;\theta) + P(y = 1 | x ; \theta) = 1\end{align*}
	$$
	</div>


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

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
Look back to the [cost function in linear regression](/machine-learning-coursera-1#cost-function).
</span>
</div>


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

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
Review the [gradient decent in linear regression](/machine-learning-coursera-1#gradient-descent).
</span>
</div>

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

"**Conjugate gradient**", "**BFGS**", and "**L-BFGS**" are <mark>more sophisticated, faster</mark> ways to optimize $\theta$ that can be used **instead of gradient descent**. We suggest that you should not write these more sophisticated algorithms yourself (unless you are an expert in numerical computing) but use the libraries instead, as they're already tested and highly optimized. <mark>Octave/Matlab provides them.</mark>

A single function that returns both $J(\theta)$ and $\frac{\partial}{\partial\theta_j}J(\theta)$

~~~ matlab
function [jVal, gradient] = costFunction(theta)
  jVal = [...code to compute J(theta)...];
  gradient = [...code to compute derivative of J(theta)...];
end
~~~

Then we can use octave's `fminunc()` optimization algorithm along with the `optimset()` function that creates an object containing the options we want to send to `fminunc()`.

~~~ python
options = optimset('GradObj', 'on', 'MaxIter', 100);
initialTheta = zeros(2,1);
[optTheta, functionVal, exitFlag] = fminunc(@costFunction, initialTheta, options);
~~~

We give to the function `fminunc()` our cost function, our initial vector of theta values, and the `options` object that we created beforehand.

<p markdown="1" class="thi-tip">
  <i class="material-icons mat-icon">info</i>
  `fmincg` works similarly to `fminunc`, but is more more efficient for dealing with a large number of parameters.
</p>

## Multiclass classification: one-vs-all

$y$ has more values than only two 0 and 1. We keep using binary classification for each group of 2 (consider one and see the others as the other group)

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
(n+1)-values $y \Rightarrow n+1$  binary classification problems. 

<div class="p-mark">
$$
\begin{align*}
y &\in \lbrace 0, 1 ... n\rbrace \\ 
h_\theta^{(0)}(x) &= P(y = 0 | x ; \theta) \\ 
h_\theta^{(1)}(x) &= P(y = 1 | x ; \theta) \\ 
\cdots & \\ 
h_\theta^{(n)}(x) &= P(y = n | x ; \theta) \\ 
\mathrm{prediction} &= \max_i( h_\theta ^{(i)}(x) )
\end{align*}
$$
</div>
</div>

<div class="col s12 l6" markdown="1">
![One vs All 1]({{img-url}}/one-vs-all-1.png){:.no-border}
</div>
</div>

<div class="p-mark" markdown="1">
After fiding `optTheta` from `fmincg`, we need to find $h_{\theta}$. From $h_{\theta}$ for all classes, we find the one with the highest propability (highest $h$). That's why we have the line of code `prediction` above.
</div>


<ul class="collapsible" data-collapsible="accordion">
<li>
<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
Why max?
</div>
<div class="collapsible-body" markdown="1">

We want to choose a $\Theta$ such that for all $j\in \\{ 0,\ldots,n \\}$, 

$$
h_{\theta}^{(j)} = P(y=j\vert x;\theta) \ge 0.5
$$

Don't forget that, we consider $h\_{\theta} \ge 0.5$ as true. Because of that, there is onlty 1 option, that's max of all $j$.
    
</div>
</li>
</ul>


<p markdown="1" class="thi-tip">
<i class="material-icons mat-icon">info</i>
See [ex 4](/machine-learning-coursera-4#exercise-programmation-multi-class-classification-and-neural-networks) for an example in practice.
</p>

## Solving the problem of overfitting

{% include download.html content="[Download Lecture 7](/files/ML-coursera/Lecture7.pdf)." %}

### The problem of overfitting

We have **many features**, $h_{\theta}$ may fit the training set very well ($J(\theta) \simeq 0$) but <mark>fail to generalize.</mark>

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Overfitting]({{img-url}}/overfitting-1.png){:.no-border}
</div>
<div class="col s12 l6" markdown="1">
![Overfitting 2]({{img-url}}/overfitting-2.png){:.no-border}
</div>
</div>

### Cost function

Options to solve:

- Reduce the number of features
	- Manually select which features to keep
	- By algorithm
- **Regularization** (<mark>add penalty terms</mark>)
	- Keep all features but reduce magnitude/values of parameters $\theta_j$
	- Works well when we have a lot of features, each of which contributes a bit to predicting $y$

![Overfitting 2]({{img-url}}/overfitting-3.png){:.no-border .w-700}

Because we need to find the **minimum**, we multiply $\theta_3, \theta_4$ by 1000 to make them very big and never be a min, i.e. they look like 0.

<div class="p-mark">
$$
J(\theta) = \frac{1}{2m} \left[ \sum_{i=1}^m (h_{\theta}(x^{(i)}) - y^{(i)})^2 + \lambda \sum_{j=1}^n \theta_j^2 \right]
$$
</div>

If $\lambda$ is **too large,** the problem of **underfitting** occurs!

### Regularized linear regression

#### Gradient Descent

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
See again GD in [linear regression](/machine-learning-coursera-1#gradient-descent), [multiple variables](/machine-learning-coursera-2#gradient-descent-for-multiple-variables) and [logistic regression](/machine-learning-coursera-3#simplified-cost-function-and-gradient-descent).
</span>
</div>

<div class="p-mark" markdown="1">
Repeat{

$$
\begin{align}
\theta_0 &:= \theta_0 - \alpha \frac{1}{m} \sum_{i=1}^m (h_{\theta}(x^{(i)}) - y^{(i)}) x_0^{(i)} \\
\theta_j &:= \theta_j(1-\alpha\frac{\lambda}{m}) - \alpha \frac{1}{m} \sum_{i=1}^m (h_{\theta}(x^{(i)}) - y^{(i)}) x_j^{(i)}, j\in \{1,\ldots, n\}
\end{align}
$$

}
</div>

Intuitively, <mark>reduce $\theta_j$ by some amount on every update</mark>, the second term is exactly the same it was before.

#### Normal equation

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
See again normal equation [linear regression](/machine-learning-coursera-2#normal-equation).
</span>
</div>

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
<div class="p-mark">
$$
\begin{align}
\theta &= (X^TX + \lambda \cdot L)^{-1} X^T y \\
L &= \begin{bmatrix} 0 & & & & \newline & 1 & & & \newline & & 1 & & \newline & & & \ddots & \newline & & & & 1 \newline\end{bmatrix}_{(n+1)\times (n+1)}
\end{align}
$$
</div>
</div>
<div class="col s12 l6" markdown="1">
- <mark>$X$ : $m\times (n+1)$ matrix</mark>
- $m$ training examples, $n$ features.
- We don't include $x_0$.
- If $m<n$ then $X^TX$ is non-invertible, but after adding $\lambda\cdot L$, <mark>$X^TX + \lambda\cdot L$ becomes invertible!</mark>
</div>
</div>


### Regularized logistic regression

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
See again [cost function for logistic regression](/machine-learning-coursera-3#cost-function).
</span>
</div>

$$
J(\theta) = - \frac{1}{m} \displaystyle \sum_{i=1}^m [y^{(i)}\log (h_\theta (x^{(i)})) + (1 - y^{(i)})\log (1 - h_\theta(x^{(i)}))]
$$

We can regularize this equation by adding a term to the end:

<div class="p-mark">
$$
J(\theta) = - \frac{1}{m} \displaystyle \sum_{i=1}^m [y^{(i)}\log (h_\theta (x^{(i)})) + (1 - y^{(i)})\log (1 - h_\theta(x^{(i)}))]
+
\dfrac{\lambda}{2m}\sum_{j=1}^n \theta_j^2.
$$
</div>

And the gradient descent

<div class="p-mark" markdown="1">
Repeat{

$$
\begin{align}
\theta_0 &:= \theta_0 - \alpha \frac{1}{m} \sum_{i=1}^m (h_{\theta}(x^{(i)}) - y^{(i)}) x_0^{(i)} \\
\theta_j &:= \theta_j(1-\alpha\frac{\lambda}{m}) - \alpha \frac{1}{m} \sum_{i=1}^m (h_{\theta}(x^{(i)}) - y^{(i)}) x_j^{(i)}, j\in \{1,\ldots, n\}
\end{align}
$$

}
</div>

The same form with GD regularized linear regression, <mark>the difference in this case is only the definition of $h_{\theta}(x)$</mark>

## Exercice de programmation: Logistic Regression

{% include download.html content="[Check instruction and explanation ex2](/files/ML-coursera/ex2.pdf)." %}

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
See again [How to submit?](/machine-learning-coursera-1#preparing-for-the-course).
</span>
</div>

### Logistic Regression

- **plotData**: Plot from `X`, `y` to separate two kind of `X`

	~~~ matlab
XPos = X(y==1, :);
XNeg = X(y==0, :);
plot(XPos(:,1), XPos(:,2), 'k+', 'LineWidth', 2, 'MarkerSize', 7);
plot(XNeg(:,1), XNeg(:,2), 'ko', 'MarkerFaceColor', 'y', 'MarkerSize', 7);
	~~~

- **sigmoid.m**: recall that

	$$
	\begin{align}
	h_{\theta}(x) &= g(\theta^Tx) \\
	g(z) &= \dfrac{1}{1+e^{-z}}
	\end{align}
	$$

	~~~ matlab
g = 1 ./ (1 + exp(-z));
	~~~

- **costFunction.m**: recall that, the cost function in logistic regression is

	$$
	J(\theta) = - \frac{1}{m} \displaystyle \sum_{i=1}^m [y^{(i)}\log (h_\theta (x^{(i)})) + (1 - y^{(i)})\log (1 - h_\theta(x^{(i)}))]
	$$

	or in vectorization,

	$$
	\begin{align*} 
	h &= g(X\theta) \\ 
	J(\theta) &= \frac{1}{m} \left(-y^{T}\log(h)-(1-y)^{T}\log(1-h)\right) 
	\end{align*}
	$$

	and **its gradient** is

	$$
	\dfrac{\partial(\theta)}{\partial\theta_j} = \dfrac{1}{m} \sum_{i=1}^m (h_{\theta}(x^{(i)}) - y^{(i)}) x_j^{(i)}, \text{ for } j=0,\ldots,n.
	$$

	or in vectorization,
	
	<div class="p-mark">
	$$
	\nabla \theta = \dfrac{1}{m} X^T(g(X\theta) - y).
	$$
	</div>

	~~~ matlab
h = sigmoid(X*theta); % hypothesis
J = 1/m * ( -y' * log(h) - (1-y)' * log(1-h) );
grad = 1/m * X' * ( h - y);
	~~~

- `fminunc`:
	- `GradObj` option to `on`, which tells fminunc that our function returns both the cost and the gradient

		~~~ matlab
	options = optimset('GradObj', 'on', 'MaxIter', 400);
		~~~

	- Notice that by using `fminunc`, you did not have to write any loops yourself, or set a learning rate like you did for gradient descent.

- **predict.m**: remember that,

	$$
	\begin{align}
	h_{\theta}(x) &= g(X\theta), \\
	h_{\theta}(x) &\ge 0.5 \to y = 1\\
	h_{\theta}(x) &< 0.5 \to y = 0
	\end{align}
	$$

	~~~ matlab
h = sigmoid(X*theta); % m x 1
p = (h >= 0.5);
	~~~

### Regularized logistic regression

**costFunctionReg.m**: recall that,

$$
J(\theta) = - \frac{1}{m} \displaystyle \sum_{i=1}^m [y^{(i)}\log (h_\theta (x^{(i)})) + (1 - y^{(i)})\log (1 - h_\theta(x^{(i)}))]
+
\dfrac{\lambda}{2m}\sum_{j=1}^n \theta_j^2.
$$

its gradient,

<div class="p-mark">
$$
\begin{align}
\dfrac{\partial J(\theta)}{\partial \theta_0}
	&= \dfrac{1}{m} \sum_{i=1}^m (h_{\theta}(x^{(i)}) - y^{(i)}) x_j^{(i)}, \text{ for } j=0 \\
\dfrac{\partial J(\theta)}{\partial \theta_j}
	&= \left( \dfrac{1}{m} \sum_{i=1}^m (h_{\theta}(x^{(i)}) - y^{(i)})x_j^{(i)} \right) + \dfrac{\lambda}{m}\theta_j, \text{ for } j\ge 1
\end{align}
$$
</div>

~~~ matlab
h = sigmoid(X*theta); % hypothesis
J = 1/m * ( -y' * log(h) - (1-y)' * log(1-h) ) + lambda/(2*m) * sum(theta(2:end).^2);

grad(1,1) = 1/m * X(:,1)' * (h-y);
grad(2:end,1) = 1/m * X(:,2:end)' * (h-y) + lambda/m * theta(2:end,1);
~~~

{% include more.html content="[Next to Week 4](/machine-learning-coursera-4)." %}
