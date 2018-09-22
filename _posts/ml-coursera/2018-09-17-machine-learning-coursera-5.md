---
title: ML Coursera 5 - Week 5
categories: [ml, it]
tags: [machine learning, ml coursera]
math: 1
toc: 1
comment: 1
date: 2018-09-22
---

{% assign img-url = '/images/posts/ML/coursera' %}

This note was first taken when I learnt the [machine learning course on Coursera](https://www.coursera.org/learn/machine-learning/).<br />
**Lectures in this week**: [Lecture 9](/files/ML-coursera/Lecture9.pdf).

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Week 4](/machine-learning-coursera-4).
</span>
</div>


{% include toc.html %}

## Cost function & Backpropagation

{% include download.html content="[Download Lecture 9](/files/ML-coursera/Lecture9.pdf)." %}

### Cost function

**Notations**

- <mark>$L$</mark> = total number of layers in network
- <mark>$s_l$</mark> = no. of units (not counting bias unit) in layer $l\in L$

**Recall**

- **Binary classification** ([review](/machine-learning-coursera-3#classification)) : 
	- $y\in \{0,1\}$, <mark>1 output unit</mark>
	- $h_{\Theta}(x)\in \mathbb{R}$
	- $s_L = 1$ (1 output unit)
	- $K=1$ ($K$ = no. of units in the output layer)
- **Multi-class classification** with $K$ classes ([review](/machine-learning-coursera-3#multiclass-classification-one-vs-all)): $y\in \mathbb{R}^K$ and <mark>K output units</mark>
	- $h_{\theta}(x) \in \mathbb{R}^K$
	- $s_L = K$ (<mark>$K\ge 3$</mark>) because if $K=2$, we can use binary classification.

**Cost function**

- **Logistic regression** (review [here](/machine-learning-coursera-3#cost-function) and [here](Regularized logistic regression)):

	<div class="p-mark">
	$$
	J(\theta) = - \frac{1}{m} \displaystyle \sum_{i=1}^m [y^{(i)}\log (h_\theta (x^{(i)})) + (1 - y^{(i)})\log (1 - h_\theta(x^{(i)}))]
	+
	\dfrac{\lambda}{2m}\sum_{j=1}^n \theta_j^2.
	$$
	</div>

- **Neural network** ([review](/machine-learning-coursera-4#neural-networks))

	<div class="p-mark">
	$$
	J(\Theta) = - \frac{1}{m} \sum_{i=1}^m \sum_{k=1}^K \left[y^{(i)}_k \log ((h_\Theta (x^{(i)}))_k) + (1 - y^{(i)}_k)\log (1 - (h_\Theta(x^{(i)}))_k)\right] + \frac{\lambda}{2m}\sum_{l=1}^{L-1} \sum_{i=1}^{s_l} \sum_{j=1}^{s_{l+1}} ( \Theta_{j,i}^{(l)})^2
	$$
	</div>

	- If we want to minimize $J(\Theta)$ as a function of $\Theta$ using one of the advanced optimization methods (fminunc, conjugate gradients, BGGS, L-BFGS, ...) we need to supply $J(\Theta)$ and the (partial) gradient derivative terms $\frac{\partial}{\partial \Theta_{ij}^{(l)}}$ for every $i,j,l$.
	- The triple sum simply adds up the squares of all the individual $\Theta$s in the entire network.
	- The $i$ in the triple sum **does not** refer to training example $i$.


### <mark>Backpropagation algorithm</mark>

Talking about an algorithm to **minize the cost function**.

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
See again [Forward propagation](/machine-learning-coursera-4#forward-propagation-vectorized-implementation).
</span>
</div>

- **Forward propagation** : from $a^{(1)}$ to the last layer $a^{(L)}$. $\Rightarrow$ computes $h_{\Theta}(x) = a^{(L)} = g(z^{(L)}) = g(\Theta^{(L-1)}a^{(L-1)})$
- **Backpropagation** : from $a^{(L)}$ back to $a^{(1)}$ $\Rightarrow$ <mark>computes the derivative (gradient)</mark>

**Notations**:

- $\delta_j^{(l)}$ = "error" of node $j$ in layer $l$.
- $a_j^{(l)}$ = activation of node $j$ in layer $l$.

For each output unit (layer $L=4$)

$$
\delta_j^{(4)} = a_j^{(4)} - y_j = (h_{\Theta})_j - y_j
$$

or **vectorization**,

$$
\delta^{(4)} = a^{(4)} - y 
$$

each vecor's **<mark>dimension</mark>** = number of output units.

![Backpropagation 1]({{img-url}}/backpropagation-1.png){:.no-border .w-700}

Keep couting $\delta^{(4)}$ to $\delta^{(2)}$. **<mark>There is no $\delta^{(1)}$</mark>** because they are our input dataset, they don't have any error!

- $\Delta_{ij}^{(l)}$ computes $\frac{\partial}{\partial\Theta_{ij}^{(l)}} J(\Theta)$.

![Backpropagation 2]({{img-url}}/backpropagation-2.png){:.no-border .w-700}

<mark>Note that</mark>, backpropagation and forward propagation are **used alternately** inside loop i.

<div class="p-mark" markdown="1">
**ALGORITHM**. For training example $t=1$ to $m$:

1. Set $a^{(1)} = x^{(t)}$
2. Compute $a^{(l)}$ for $l=2,3,\ldots,L$ using **forward propagation**

	$$
	\begin{align}
	z^{l+1} &= \Theta^{(l)}a^{(l)} \\
	a^{(l+1)} &= g(z^{(l+1)}) \quad (\text{add } a^{(l)}_0)\\
	...& \\
	a^{(L)} &= h_{\Theta}(x) = g(z^{(L)})
	\end{align}
	$$

3. Using $y^{(t)}$, compute

	$$
	\delta^{L} = a^{(L)} - y^{(t)}
	$$

	where, $L$ = total number of layers, $a^{(L)}$ = is the vector of outputs of the activation units for the last layer. So, $\delta^{(L)}$ the differences of our actual results in the last layer and the correct outputs in $y$.

4. Compute $\delta^{(L-1)},\ldots,\delta^{(2)}$ using,

	$$
	\delta^{(l)} = ((\Theta^{(l)})^T \delta^{(l+1)}) .* a^{(l)} .* (1-a^{(l)})
	$$

5. $\Delta_{ij}^{(l)} = \Delta_{ij}^{(l)} + a_j^{(l)}\delta_i^{(l+1)}$ or with vectorization 

	$$
	\Delta^{(l)} = \Delta^{(l)} + \delta^{(l+1)} (a^{(l)})^T
	$$

	Hence, we update our new $\Delta$ matrix,

	$$
	\begin{align}
	D_{i,j}^{(l)} &:= \frac{1}{m} (\Delta_{i,j}^{(l)} + \lambda\Theta^{(l)}_{i,j}), \quad \text{if } j\ne 0 \\
	D_{i,j}^{(l)} &:= \frac{1}{m} \Delta_{i,j}^{(l)}, \quad \text{if } j= 0
	\end{align}
	$$

6. Finally, we get

	$$
	\dfrac{\partial}{\partial\Theta_{ij}^{(l)}} J(\Theta)  = D_{ij}^{(l)}.
	$$

</div>

### Backpropagation intuition





## Backpropagation in practice

### Implementation note: Unrolling parameters

### Gradient checking

### Randon initialization

### Putting it together



## Application of Neural networks





## Exercise de programmation: Neural network learning








