---
title: ML Coursera 5 - Week 5
categories: [ml, it]
tags: [machine learning, ml coursera]
math: 1
toc: 1
comment: 1
date: 2018-09-25
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

<div class="p-mark">
$$
\delta_j^{(4)} = a_j^{(4)} - y_j = (h_{\Theta})_j - y_j
$$
</div>

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

#### Algorithm

<div  class="thi-step">
<div class="step">
<div class="step-number"></div>
<div class="step-content" markdown="1">
Set $a^{(1)} = x^{(t)}$
</div>
</div>

<div class="step">
<div class="step-number"></div>
<div class="step-content" markdown="1">
Compute $a^{(l)}$ for $l=2,3,\ldots,L$ using **forward propagation**

<div class="p-mark">
$$
\begin{align}
z^{l+1} &= \Theta^{(l)}a^{(l)} \\
a^{(l+1)} &= g(z^{(l+1)}) \quad (\text{add } a^{(l)}_0)\\
...& \\
a^{(L)} &= h_{\Theta}(x) = g(z^{(L)})
\end{align}
$$
</div>

</div>
</div>

<div class="step">
<div class="step-number"></div>
<div class="step-content" markdown="1">
Using $y^{(t)}$, compute

$$
\delta^{L} = a^{(L)} - y^{(t)}
$$

where, $L$ = total number of layers, $a^{(L)}$ = is the vector of outputs of the activation units for the last layer. So, $\delta^{(L)}$ the differences of our actual results in the last layer and the correct outputs in $y$.
</div>
</div>

<div class="step">
<div class="step-number"></div>
<div class="step-content" markdown="1">
Compute $\delta^{(L-1)},\ldots,\delta^{(2)}$ using,

<div class="p-mark">
$$
\delta^{(l)} = ((\Theta^{(l)})^T \delta^{(l+1)}) .* a^{(l)} .* (1-a^{(l)})
$$
</div>

</div>
</div>

<div class="step">
<div class="step-number"></div>
<div class="step-content" markdown="1">
$\Delta_{ij}^{(l)} = \Delta_{ij}^{(l)} + a_j^{(l)}\delta_i^{(l+1)}$ or with vectorization 

<div class="p-mark">
$$
\Delta^{(l)} = \Delta^{(l)} + \delta^{(l+1)} (a^{(l)})^T
$$
</div>

Hence, we update our new $\Delta$ matrix,

<div class="p-mark">
$$
\begin{align}
D_{i,j}^{(l)} &:= \frac{1}{m} (\Delta_{i,j}^{(l)} + \lambda\Theta^{(l)}_{i,j}), \quad \text{if } j\ne 0 \\
D_{i,j}^{(l)} &:= \frac{1}{m} \Delta_{i,j}^{(l)}, \quad \text{if } j= 0
\end{align}
$$
</div>

</div>
</div>

<div class="step">
<div class="step-number"></div>
<div class="step-content" markdown="1">
Finally, we get

<div class="p-mark">
$$
\dfrac{\partial}{\partial\Theta_{ij}^{(l)}} J(\Theta)  = D_{ij}^{(l)}.
$$
</div>

</div>
</div>

</div>

### Backpropagation intuition

$$
\delta_j^{(l)} = \dfrac{\partial}{\partial z_j^{(l)}} \text{cost}(t).
$$

![Backpropagation 3]({{img-url}}/backpropagation-3.png){:.no-border .w-700}

## Backpropagation in practice

### Implementation note: Unrolling parameters

Example: 

$$
\Theta^{(1)} \in \mathbb{R}^{10\times 11}, 
\Theta^{(2)} \in \mathbb{R}^{10\times 11},
\Theta^{(3)} \in \mathbb{R}^{1\times 11},\\
D^{(1)} \in \mathbb{R}^{10\times 11},
D^{(2)} \in \mathbb{R}^{10\times 11},
D^{(3)} \in \mathbb{R}^{1\times 11}
$$

~~~ matlab
% make a long vector 
thetaVec = [ Theta1(:); Theta2(:); Theta3(:) ];
DVec = [ D1(:); D2(:); D3(:) ]
~~~

If we want to "roll" (get back to each theta),

~~~ matlab
Theta1 = reshape( thetaVec(1:110), 10, 11 );
Theta2 = reshape( thetaVec(111:220), 10, 11 );
Theta3 = reshape( thetaVec(221:230), 1, 11 );
~~~

<div class="p-mark" markdown="1">
![Learning Algorithm 1]({{img-url}}/learning-algorithm-1.png){:.no-border .w-700}
</div>


### Gradient checking

When implement with backpropagation, there are some subtle error that we don't know and cannot recognize in which they seems to be right but not. That why we **need to always implement gradient checking** when working with complex models.

<div class="p-mark">
$$
\dfrac{d}{d\Theta} J(\Theta) = \dfrac{J(\Theta + \epsilon) - J(\Theta - \epsilon)}{2\epsilon}
$$
</div>

We usually choose $\epsilon = 10^{-4}$.

Implement,

~~~ matlab
gradApprox = (J(theta + EPSILON) - J(theta - EPSILON)) / (2*EPSILON)
~~~


<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
![Gradient checking 1]({{img-url}}/gradient-checking-1.png){:.no-border}
</div>
<div class="col s12 l6" markdown="1">
![Gradient checking 2]({{img-url}}/gradient-checking-2.png){:.no-border}
</div>
</div>

~~~ matlab
epsilon = 1e-4;
for i = 1:n,
  thetaPlus = theta;
  thetaPlus(i) += epsilon;
  thetaMinus = theta;
  thetaMinus(i) -= epsilon;
  gradApprox(i) = (J(thetaPlus) - J(thetaMinus))/(2*epsilon)
end;
~~~

If we have `gradApprox` $\simeq$ `DVec`, we can be more confident on the result of `DVec` and other computations after that.

<div class="p-mark" markdown="1">

- Implement `DVec`
- Imlement `gradApprox`
- Make sure they have similar values.
- <mark>Turn of gradient checking</mark> and only **use backprop code for learning**.

</div>


### Randon initialization

We **cannot use** initial of $\Theta$ as `initialTheta = zeros(n,1)` because it will leads to the fact that all $a^{(l)}_j$ are equal too.

We need to initialize $\Theta_{ij}^{(l)}$ to a random values in $[-\epsilon, \epsilon]$, i.e.

<div class="p-mark">
$$
-\epsilon \le \Theta_{ij}^{(l)} \le \epsilon.
$$
</div>

~~~ matlab
Theta1 = rand(10,11) * (2 * INIT_EPSILON) - INIT_EPSILON;
Theta2 = rand(10,11) * (2 * INIT_EPSILON) - INIT_EPSILON;
Theta3 = rand(1,11) * (2 * INIT_EPSILON) - INIT_EPSILON;
~~~

### <mark>Putting it together</mark>

1. **Choose a network architecture**: choose the number of hidden layers.
	- *No. of input units*: dim of features $x^{(i)}$
	- *No. of output units*: number of classes. Note that, we need to write $y$ is the set of separated unit vectors like $y=[1,0,...,0]^T$ or $y=[0,1,0,...,0]^T$,...
	- *No. of hidden units*: 1 (defaults). If $>1$, should choose <mark>the same</mark> number of units for each hidden layer.
	- More hidden units $\Rightarrow$ better but more complicated!
2. **Training a neural network**: 
	1. Random initialize weights : small near zero.
	2. Implement [forward propagation](/machine-learning-coursera-4#forward-propagation-vectorized-implementation) to get $h_{\Theta}(x^{(i)})$ from $x^{(i)}$
	3. Implement code to compute cost function $J(\Theta)$
	4. Implement backprop to compute partial derivatives $\frac{\partial}{\partial\Theta_{jk}^{(l)}}J(\Theta)$.

		Need to use `foor-loop` through all of $(x^{(i)}, y^{(i)})$ for `i=1:m`. **Should do that** instead of not using it (Andrew recommend!!!).

		![Backpropagation 4]({{img-url}}/backpropagation-4.png){:.no-border .w-700}
	5. Use gradient checking to compare $\frac{\partial}{\partial \Theta_{jk}^{(l)}}J(\Theta)$ computed using backprop vs. using numerical estimate of gradient of $J(\Theta)$. **Don't forget to disable gradient checking code!!!**
	6. Use gradient descent or advanced optimization method with backprop to try to minimize $J(\Theta)$ as a function of $\Theta$.

	On neural network, cost function is **non convex**. Therefore, methods can (**theoritically**) stuck on local optimal. But **in practice**, it's **not a huge problem**!

## Application of Neural networks





## Exercise de programmation: Neural network learning








