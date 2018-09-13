---
title: ML Coursera 4 - Week 4
categories: [ml, it]
tags: [machine learning, ml coursera]
math: 1
toc: 1
comment: 1
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

- Algorithms try to mimic the brain.
- 80s, 90s (very old)
- **activation function** = sigmoid (logistic) $g(z)$
- (sometimes) $\theta$ called **weights** parameters
- Neural network: first layer (**input layer**), intermidiate layers (**hidden layer**) and the last layer (**output layer**)

	![Neural network 1]({{img-url}}/neural-network-1.png){:.no-border .w-600}

- **Notations**:
	- $a_i^{(j)}$ = "activation" of unit $i$ in layer $j$
	- $\Theta^{(J)}$ = matrix of weights controlling function mapping from layer $j$ to layer $j+1$
	- $\Theta \in \mathbb{R}^{m\times n+1}$ where $m$ = number of unit in current layer, $n$ = number of units in previous layer (not include unit 0).

		![Neural network 2]({{img-url}}/neural-network-2.png){:.no-border .w-800}

		<div class="p-mark">
		$$
		\begin{align}
		\Theta^{(\text{previous})} &: \text{previous layer} \to \text{current layer} \\
		\Theta^{(\text{previous})} &\in \mathbb{R}^{\text{current} \times (\text{previous}+1)}
		\end{align}
		$$
		</div>

### Forward propagation: vectorized implementation

![Neural network 2]({{img-url}}/neural-network-2.png){:.no-border .w-800}

<div class="p-mark">
$$
\begin{align}
z^{(2)} &= \theta^{(1)} a^{(1)}\\ 
a^{(2)} &= g(z^{(2)})
\end{align}
$$
</div>

- Neural network is look like logistic regression, **except** that instead of using $x_1, x_2, \ldots$, it's using $a^{(j)}_1, a^{(j)}_2, \ldots$
- Neural network learning its own features.
- **Architectures** = how different neurons connected to each other.
- <mark>Final</mark>

	<div class="p-mark">
	$$
	h_{\theta}(x) = a^{j+1} = g(z^{j+1}).
	$$
	</div>

## Examples and Intuitions I

## Examples and Intuitions II

## Exercise Programmation: Multi-class Classification and Neural Networks
