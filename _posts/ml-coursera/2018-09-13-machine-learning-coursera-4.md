---
title: ML Coursera 4 - Week 4
categories: [ml, it]
tags: [machine learning, ml coursera]
math: 1
toc: 1
comment: 1
date: 2018-09-16
---

{% assign img-url = '/images/posts/ML/coursera' %}

This note was first taken when I learnt the [machine learning course on Coursera](https://www.coursera.org/learn/machine-learning/).<br />
**Lectures in this week**: [Lecture 8](/files/ML-coursera/Lecture8.pdf).

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Week 3](/machine-learning-coursera-3).
</span>
</div>

{% include toc.html %}

## Neural Networks

{% include download.html content="[Download Lecture 8](/files/ML-coursera/Lecture8.pdf)." %}

- Algorithms try to mimic the brain.
- 80s, 90s (very old)
- **<mark>activation function</mark>** = sigmoid (logistic) $g(z)$
- (sometimes) $\theta$ called **weights** parameters
- Neural network: first layer (**input layer**), intermidiate layers (**hidden layer**) and the last layer (**output layer**)

	![Neural network 1]({{img-url}}/neural-network-1.png){:.no-border .w-600}

- **Notations**:
	- $a_i^{(j)}$ = "activation" of unit $i$ in layer $j$

		<div class="p-mark">
		$$
		a_{\text{unit}}^{(\text{layer})}
		$$
		</div>

	- $\Theta^{(j)}$ = matrix of weights controlling function mapping from layer $j$ to layer $j+1$
	- $\Theta \in \mathbb{R}^{m\times n+1}$ where $m$ = number of unit in current layer, $n$ = number of units in previous layer (not include unit 0).

		<div class="p-mark">
		$$
		\begin{align}
		\Theta^{(\text{previous})} &: \text{previous layer} \to \text{current layer} \\
		\Theta^{(\text{previous})} &\in \mathbb{R}^{\text{current} \times (\text{previous}+1)}
		\end{align}
		$$
		</div>

		![Neural network 2]({{img-url}}/neural-network-2.png){:.no-border .w-800}

		<div class="p-mark">
		$$
		a_{k\in \text{current units}}^{(\text{current layer})}
		= g\left( \sum_{i\in \text{prev units}} \Theta_{ki}^{(\text{prev layer})} a_i^{(\text{prev layer})} \right)
		$$
		</div>

### <mark>Forward propagation</mark>: vectorized implementation

![Neural network 3]({{img-url}}/neural-network-3.png){:.no-border .w-800}

<div class="p-mark">
$$
\begin{align}
z^{(2)} &= \Theta^{(1)} a^{(1)}\\ 
a^{(2)} &= g(z^{(2)})
\end{align}
$$
</div>

- Neural network is look like logistic regression, **except** that instead of using $x_1, x_2, \ldots$, it's using $a^{(j)}_1, a^{(j)}_2, \ldots$
- Neural network learning its own features.
- **Architectures** = how different neurons connected to each other.
- **<mark>Final</mark>**

	<div class="p-mark">
	$$
	\begin{align}
	h_{\theta}(x) = a^{(j+1)} = g(z^{(j+1)}) = g(\Theta^{(j)}a^{(j)}).
	\end{align}
	$$
	</div>

## Examples and Intuitions I

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Neural network 4]({{img-url}}/neural-network-4.png){:.no-border}
</div>
<div class="col s12 l6" markdown="1">
![Neural network 5]({{img-url}}/neural-network-5.png){:.no-border}
</div>
</div>

## Examples and Intuitions II

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Neural network 6]({{img-url}}/neural-network-6.png){:.no-border}
</div>
<div class="col s12 l6" markdown="1">
![Neural network 7]({{img-url}}/neural-network-7.png){:.no-border}
</div>
</div>

## Multiclass classification

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Neural network 8]({{img-url}}/neural-network-8.png){:.no-border}
</div>
<div class="col s12 l6" markdown="1">
![Neural network 9]({{img-url}}/neural-network-9.png){:.no-border}
</div>
</div>****

## Exercise Programmation: Multi-class Classification and Neural Networks

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
See again [Multiclass classification: one-vs-all](/machine-learning-coursera-3#multiclass-classification-one-vs-all).
</span>
</div>

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
See again [Advanced Optimization](/machine-learning-coursera-3#advanced-optimization).
</span>
</div>

- `lrCostFunction.m`

  This ex is the same with the one in the previous week.

  ~~~ matlab
  h = sigmoid(X*theta); % hypothesis
  J = 1/m * ( -y' * log(h) - (1-y)' * log(1-h) ) + lambda/(2*m) * sum(theta(2:end).^2);
  
  grad(1,1) = 1/m * X(:,1)' * (h-y);
  grad(2:end,1) = 1/m * X(:,2:end)' * (h-y) + lambda/m * theta(2:end,1);
  ~~~

- `oneVsAll.m`

  ~~~ matlab
  initial_theta = zeros(n + 1, 1);
  options = optimset('GradObj', 'on', 'MaxIter', 50);
  for c = 1:num_labels
  	  [theta] = fmincg (@(t)(lrCostFunction(t, X, (y == c), lambda)), initial_theta, options);
  	  all_theta(c,:) = theta(:);
  end
  ~~~

  <p markdown="1" class="thi-tip">
    <i class="material-icons mat-icon">info</i>
    `fmincg` works similarly to `fminunc`, but is more more efficient for dealing with a large number of parameters.
  </p>

- `predictOneVsAll.m`

    ~~~ matlab
  h = X * all_theta';
  [~, p] = max(h,[],2);
    ~~~

- `predict.m` : "you implemented multi-class logistic regression to recognize handwritten digits. However, logistic regression cannot form more complex hypotheses as it is only a linear classifier."

	~~~ matlab
	X = [ones(m, 1) X]; % add column 1 to a2
	z2 = X * Theta1';
	a2 = sigmoid(z2);
	a2 = [ones(m, 1) a2]; % add column 1 to a2
	h = a2 * Theta2';
	[~, p] = max(h,[],2);
	~~~










