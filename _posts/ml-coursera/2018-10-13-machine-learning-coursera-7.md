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

<div class="p-mark" markdown="1">
From this note, I see that this note is really detailed so that I can use it for the future reference. I have set the backup for this [week7 here](/files/ML-coursera/notes/SVM.pdf).
</div>

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

- So we get (new **SVM cost function**)

  $$
  \min \dfra{1}{m}\left[ \sum_{i=1}^m y^{(i)} cost_1(\Theta%Tx^{(i)}) + (1-y^{(i)})cost_0(\Theta^Tx^{(i)}) \right] + \dfrac{\lambda}{2m}\sum_{i=1}^n \theta^2_j
  $$

- We use another notation to minimize problem

  $$
  \min_{\Theta} C \sum_{i=1}^m \left[ \sum_{i=1}^m y^{(i)} cost_1(\Theta%Tx^{(i)}) + (1-y^{(i)})cost_0(\Theta^Tx^{(i)}) \right] + \dfrac{1}{2}\sum_{i=1}^n \theta^2_j
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

- 

### Mathematics behind large classification

## Kernels

### Kernels I

### Kernels II

## SVMs in practice

### Using an SVM

## Programming Assignment

