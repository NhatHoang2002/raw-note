---
title: "ML Coursera 7 - Week 7: Support Vector Machines"
categories: [ml, it]
tags: [machine learning, ml coursera]
math: 1
toc: 1
comment: 1
date: 2018-10-17
---

{% assign img-url = '/images/posts/ML/coursera' %}

This note was first taken when I learnt the [machine learning course on Coursera](https://www.coursera.org/learn/machine-learning/).<br />
**Lectures in this week**: [Lecture 12](/files/ML-coursera/Lecture12.pdf).

<p markdown="1" class="thi-tip">
<i class="material-icons mat-icon">error</i>
From this note, I see that [this note](/files/ML-coursera/note/) of [Alex Holehouse](http://holehouse.org/) is really detailed so that I can use it for the future reference. I don't have enough time for noting as previous note.
</p>

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Week 6](/machine-learning-coursera-6).
</span>
</div>


{% include toc.html %}

- So far, we've seen a range of different algorithms
  - With supervised learning algorithms - performance is pretty similar. What matters more often is:
    - The amount of training data
    - Skill of applying algorithms
- One final supervised learning algorithm that is **widely used** - **support vector machine (SVM)**
  - Compared to both logistic regression and neural networks, <mark>a SVM sometimes gives a cleaner way of learning non-linear functions</mark>
  - Later in the course we'll do a survey of different supervised learning algorithms

## Large margin classification

### Optimization objective

- Alternative view of logistic regression: we see the cost function is a function of $z=X\Theta$.
- To build a SVM we must redefine our cost functions
  - Instead of a curved line create two straight lines (magenta) which acts as **an approximation to the logistic regression** $y = 1$ function
  - So here we define the two cost function terms for our SVM graphically

  ![Two new cost functions]({{img-url}}/svm-1.png){:.no-border .w-700}

  <div class="p-mark">
  $$
  \begin{align}
  cost_0 &= -\log(1-\dfrac{1}{1+e^{-z}}) \\
  cost_1 &= -\log(\dfrac{1}{1+e^{-z}})
  \end{align}
  $$
  </div>

- So we get (new **SVM cost function**)

  $$
  \min \dfrac{1}{m}\left[ \sum_{i=1}^m y^{(i)} cost_1(\Theta^Tx^{(i)}) + (1-y^{(i)})cost_0(\Theta^Tx^{(i)}) \right] + \dfrac{\lambda}{2m}\sum_{i=1}^n \theta^2_j
  $$

- We use another notation to minimize problem

  $$
  \min_{\Theta} C \sum_{i=1}^m \left[ \sum_{i=1}^m y^{(i)} cost_1(\Theta^Tx^{(i)}) + (1-y^{(i)})cost_0(\Theta^Tx^{(i)}) \right] + \dfrac{1}{2}\sum_{i=1}^n \theta^2_j
  $$

- Unlike logistic, $h_{\theta}(x)$ doesn't give us a probability, but instead we get a direct prediction of 1 or 0 (as mentioned before)


### Large margin intuition 

- Logistic regression only need $X\Theta\ge 0$ to get $h=1$ or $X\Theta <0$ to get $0$. SVM gives us a clearer way ($X\Theta \ge 1$ and $X\Theta <-1$ respectively).

  ![Support vector machine]({{img-url}}/svm-2.png){:.no-border .w-700}

- Consider a case in which $C$ very huge, we need to choose $\Theta$ such that $A=0$ ($A$ in $CA+B$).
  - If $y1$, we need to find $\Theta$ such that $X\Theta \ge 1$
  - If $y=0$, find $\Theta$ such that $X\Theta <-1$
- When $CA=0$, the minimization problem becomes,

  ![SVM 3]({{img-url}}/svm-3.png){:.no-border .w-500}

- Mathematically, that black line has a **larger minimum distance (margin)** from any of the training examples

  ![Larger minimum distance]({{img-url}}/svm-4.png){:.no-border .w-500}

### Mathematics behind large classification

## Kernels

### Kernels I

- That a hypothesis computes a decision boundary by taking the sum of the parameter vector multiplied by a new feature vector f, which simply contains the various high order x terms

  $$
  \begin{align}
  h_{\theta}(x) &= \theta_0 + \theta_1f_1 + \theta_2 + \ldots, \\
  f_1 &= x_1, f_2 = x_1x_2, \ldots
  \end{align}
  $$

- We choose **landmarks** $l^{(1)}, l^{(2)}, \ldots$ and then using the **<mark>similarity</mark>** (_kernel_) between $x$ and each landmark $l^{(i)}$.

  <div class="p-mark">
  $$
  \begin{align}
  \text{similarity} = k(x,l^{(i)}) &= \text{exp}\left( -\dfrac{\Vert x-l^{(i)}\Vert^2}{2\sigma^2} \right) \\
  f_i &:=  \text{similarity}(x,l^{(i)}).
  \end{align}
  $$
  </div>

  - $\sigma$: standard deviation
  - $\sigma^2$: variance.
  - $\Vert \cdot \Vert$: Euclidean distance

  $$
  \Vert x-l^{(i)}\Vert^2 = \sum_{j=1}^n (x_j-l_j^{(i)})
  $$

  - There are many **kernels**, above def of similarity is** Gaussian kernel**.

  ![Kernel and similarity]({{img-url}}/kernel-1.png){:.no-border .w-600}

  - We call $f$ landmark also!

### Kernels II

- Where do we get the landmarks from?
- For each example place a **landmark at exactly the same location**
  - Given $m$ examples of $n$ features $(x^{(i)}, y^{(i)}$ for $i=1,m$.
  - Choose landmarks: $l^{(i)} = x^{(i)}$ where $i=1,m$.
  - We will build $n$ landmark $f^{(i)}$, each of them is built from

  $$
  f_k^{(i)} = k(x^{(i)}, l^{(k)}), \text{ for } k=1,m.
  $$

- <mark>Note that</mark> $m$ input elements $x^{(i)}$ becomes $m+1$ landmarks $f$ ($f^{0} = 1$)
- $\Theta$ now becomes $\Theta \in \mathbb{R}^{(m+1)\times 1}$.
- $f\in \mathbb{R}^{(m+1)}$ also.
- <mark>Predict $1$ if $\Theta^Tf \ge 0$</mark>
- **SVM learning algorithm**

  <div class="p-mark">
  $$
    \min_{\Theta} C\sum_{i=1}^m \left( y^{(i)} cost_1 (\Theta^Tf^{(i)}) + (1-y^{(i)})cost_0(\Theta^Tf^{(i)})\right) 
      + \dfrac{1}{2}\sum_{j=1}^m\phi_j^2, \quad (n=m \text{ in this case})
  $$
  </div>

- We minimize using $f$ as the feature vector instead of $x$
- <mark>$m=n$</mark> because number of features is the number of training data examples we have.
- It's really expensive because there may be a lot of features (= number of training examples). <mark>It's good to use shelf software to minimize this function</mark> instead. DON'T write your own software to do that!!
- **Variance vs Bias trade-off**
  - Large $C$ ($\frac{1}{\lambda}$): low bias, high variance $\Rightarrow$ overfitting.
  - Small C gives a hypothesis of high bias low variance $\Rightarrow$ underfitting
  - Large $\sigma^2$: f features vary more smoothly - higher bias, lower variance
  - Small $\sigma^2$: f features vary unexpectedly - low bias, high variance

## SVMs in practice

### Using an SVM

## Programming Assignment

