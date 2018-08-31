---
title: ML Coursera 1 - Week 1
categories: [ml, it]
tags: [machine learning, ml coursera]
math: 1
toc: 1
date: 2018-08-31
---

{% assign img-url = '/images/posts/ML/coursera' %}

This note was fist taken when I learnt the [machine learning course on Coursera](https://www.coursera.org/learn/machine-learning/).

{% include toc.html %}

{% include more.html content="[Go to Week 2](/machine-learning-coursera-2)." %}

## Preparing for the course

- [Discussion forums](https://www.coursera.org/learn/machine-learning/discussions).
- Check [server down or not](https://status.coursera.org/).
- [Frequently asked questions](https://www.coursera.org/learn/machine-learning/supplement/gBboB/frequently-asked-questions)
- Slides : [Lecture 1]({{site.baseurl}}/files/ML-coursera/Lecture1.pdf) (Introduction), [Lecture 2]({{site.baseurl}}/files/ML-coursera/Lecture2.pdf) (Model & Cost function, Parameter learning), [Lecture 3]({{site.baseurl}}/files/ML-coursera/Lecture3.pdf) (Linear Algebra).
- [All videos](https://youtu.be/PPLop4L2eGk) in course on Youtube.
- Assignment must be done with Octave or Matlab.
- You need a Matlab account and you can use it (free version for this course only): [Go to Matlab Online](https://matlab.mathworks.com/){:target="_blank"}, read more [here](https://www.coursera.org/learn/machine-learning/supplement/rANSM/accessing-matlab-online-and-uploading-the-exercise-files).

## Introduction

{% include more.html content="[Download Lecture 1](/files/ML-coursera/Lecture1.pdf)." %}

### What is ML?

Two definitions of Machine Learning are offered. Arthur Samuel described it as: "the field of study that <mark>gives computers the ability to learn without being explicitly programmed.</mark>" This is an older, informal definition.

Tom Mitchell provides a more modern definition: <mark>"A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E."</mark>

Example: playing checkers.

- E = the experience of playing many games of checkers
- T = the task of playing checkers.
- P = the probability that the program will win the next game.

In general, any machine learning problem can be assigned to one of two broad classifications: **Supervised learning** and **Unsupervised learning**.

### Supervised Learning

In supervised learning, we are given a data set and already know what our correct output should look like, having the idea that there is a relationship between the input and the output. Supervised learning problems are categorized into **regression** and **classification** problems. 

- In a **regression problem**, we are trying to predict results within a <mark>continuous output</mark>, meaning that we are trying to map input variables to some continuous function. 
- In a **classification problem**, we are instead trying to predict results in a <mark>discrete output</mark>. In other words, we are trying to map input variables into discrete categories.

**Examples**:

- **Example 1**: Given data about the size of houses on the real estate market, try to predict their price. Price as a function of size is a continuous output, so this is a regression problem. We could turn this example into a classification problem by instead making our output about whether the house "sells for more or less than the asking price." Here we are classifying the houses based on price into two discrete categories.

- **Example 2**:

    (a) Regression - Given a picture of a person, we have to predict their age on the basis of the given picture

    (b) Classification - Given a patient with a tumor, we have to predict whether the tumor is malignant or benign.

### Unsupervised Learning

Unsupervised learning allows us to approach <mark>problems with little or no idea what our results should look like</mark>. We can derive structure from data where we don't necessarily know the effect of the variables.

We can derive this structure by clustering the data based on relationships among the variables in the data.

With unsupervised learning there is no feedback based on the prediction results.

Example:

- **Clustering**: Take a collection of 1,000,000 different genes, and find a way to automatically group these genes into groups that are somehow similar or related by different variables, such as lifespan, location, roles, and so on.

- **Non-clustering**: The "Cocktail Party Algorithm", allows you to find structure in a chaotic environment. (i.e. identifying individual voices and music from a mesh of sounds at a cocktail party).

## Model and Cost function

{% include more.html content="[Download Lecture 2](/files/ML-coursera/Lecture2.pdf)." %}

### Model Representation

To establish notation for future use, we’ll use $x^{(i)}$ to denote the “input” variables (living area in this example), also called input features, and $y^{(i)}$ to denote the “output” or target variable that we are trying to predict (price). A pair $(x^{(i)} , y^{(i)} )$ is called a training example, and the dataset that we’ll be using to learn—a list of m training examples $(x(i),y(i))$; $i=1,\ldots,m—is$ called a training set. Note that the superscript “$(i)$” in the notation is simply an index into the training set, and has nothing to do with exponentiation. We will also use $X$ to denote the space of input values, and $Y$ to denote the space of output values. In this example, $X = Y = \mathbb{R}$.

To describe the supervised learning problem slightly more formally, our goal is, given a training set, to learn a function $h : X \to Y$ so that $h(x)$ is a “good” predictor for the corresponding value of $y$. For historical reasons, this function $h$ is called a hypothesis. Seen pictorially, the process is therefore like this:

<div class="p-mark" markdown="1">
When the target variable that we’re trying to predict is **continuous**, such as in our housing example, we call the learning problem a **regression problem**. When $y$ can take on only a **small number of discrete values** (such as if, given the living area, we wanted to predict if a dwelling is a house or an apartment, say), we call it a **classification problem**.
</div>

### Cost function

We can **measure the accuracy of our hypothesis function** by using a **cost function**. This takes an average difference (actually a fancier version of an average) of all the results of the hypothesis with inputs from x's and the actual output y's.

$$
\begin{align}
J(\theta_0, \theta_1) = \dfrac {1}{2m} \displaystyle \sum _{i=1}^m \left ( \hat{y}_{i}- y_{i} \right)^2 = \dfrac {1}{2m} \displaystyle \sum _{i=1}^m \left (h_\theta (x_{i}) - y_{i} \right)^2
\end{align}
$$


To break it apart, it is $\frac{1}{2}\bar{x}$ is the mean of the squares of $h_\theta (x_{i}) - y_{i}h$, or the difference between the predicted value and the actual value.

This function is otherwise called the "**Squared error function**", or "**Mean squared error**". The mean is halved $\frac{1}{2}$ as a convenience for the computation of the gradient descent, as the derivative term of the square function will cancel out the $\frac{1}{2}$ term. The following image summarizes what the cost function does:

![Cost function]({{img-url}}/cost-function.png){:.no-border}

### Cost function intuition I (one variable)

If we try to think of it in visual terms, our training data set is scattered on the x-y plane. We are trying to make a straight line (defined by $h_{\theta}(x)$ which passes through these scattered data points.

Our objective is to get the best possible line. The best possible line will be such so that the average squared vertical distances of the scattered points from the line will be the least. Ideally, the line should pass through all the points of our training data set. In such a case, the value of $J(\theta_0, \theta_1)$ will be 0. The following example shows the ideal situation where we have a cost function of 0.

![Cost function intuition 1]({{img-url}}/cost-function-1.png){:.no-border .w-600}

When $\theta_1 = 1$, we get a slope of 1 which goes through every single data point in our model. Conversely, when $\theta_1 = 0.5$, we see the vertical distance from our fit to the data points increase.

![Cost function intuition 2]({{img-url}}/cost-function-2.png){:.no-border .w-600}

This increases our cost function to 0.58. Plotting several other points yields to the following graph:

![Cost function intuition 3]({{img-url}}/cost-function-3.png){:.no-border}

Thus as a goal, we should try to minimize the cost function. In this case, $\theta_1 = 1$ is our global minimum.


### Cost function intuition II (two variables)

A **contour plot** is a graph that contains many contour lines. A contour line of a two variable function has a constant value at all points of the same line. An example of such a graph is the one to the right below.

![Cost function intuition 2-1]({{img-url}}/cost-function-2-1.png){:.no-border}

Taking any color and <mark>going along the 'circle', one would expect to get the same value of the cost function</mark>. For example, the three green points found on the green line above have the same value for $J(\theta_0,\theta_1)$ and as a result, they are found along the same line. The circled $x$ displays the value of the cost function for the graph on the left when $\theta_0=800, \theta_1= -0.15$. Taking another h(x) and plotting its contour plot, one gets the following graphs:

![Cost function intuition 2-2]({{img-url}}/cost-function-2-2.png){:.no-border}

When $\theta_0 = 360$ and $\theta_1=0$, the value of $J(\theta_0,\theta_1)$ in the contour plot gets closer to the center thus reducing the cost function error. Now giving our hypothesis function a slightly positive slope results in a better fit of the data.

![Cost function intuition 2-3]({{img-url}}/cost-function-2-3.png){:.no-border}

The graph above minimizes the cost function as much as possible and consequently, the result of $\theta_1$ and $\theta_0$ tend to be around 0.12 and 250 respectively. Plotting those values on our graph to the right seems to put our point in the center of the inner most 'circle'.

## Parameter learning

### Gradient descent

<div class="p-mark">
Algorithm to minimizing the cost function $J$.
</div>

So we have our hypothesis function and we have a way of measuring how well it fits into the data. Now we need to estimate the parameters in the hypothesis function. That's where gradient descent comes in.

Imagine that we graph our hypothesis function based on its fields $\theta_0, \theta_1$  (actually we are graphing the cost function as a function of the parameter estimates). We are not graphing x and y itself, but the parameter range of our hypothesis function and the cost resulting from selecting a particular set of parameters.

We put $\theta_0$ on the x axis and $\theta_1$  on the y axis, with the cost function on the vertical z axis. The points on our graph will be the result of the cost function using our hypothesis with those specific theta parameters. The graph below depicts such a setup.

![Gradient descent 1]({{img-url}}/gradient-descent-1.png){:.no-border}

We will know that we have succeeded when our cost function is at the very bottom of the pits in our graph, i.e. when its value is the minimum. The red arrows show the minimum points in the graph.

**The way we do this is by taking** the derivative (the tangential line to a function) of our cost function. <mark>The slope of the tangent is the derivative at that point and it will give us a direction to move towards</mark>. We make steps down the cost function in the direction with the **steepest descent**. The size of each step is determined by the parameter $\alpha$, which is called the **<mark>learning rate</mark>**.

For example, the distance between each 'star' in the graph above represents a step determined by our parameter $\alpha$. A smaller $\alpha$ would result in a smaller step and a larger $\alpha$ results in a larger step. The direction in which the step is taken is determined by the partial derivative of $J(\theta_0,\theta_1)$. **Depending on where one starts on the graph, one could end up at different points**. The image above shows us two different starting points that end up in two different places.

The gradient descent algorithm is:

<div class="p-mark">
Repeat until convergence:

$$
\theta_j := \theta_j - \alpha \dfrac{\partial}{\partial \theta_j} J(\theta_0, \theta_1),
$$

where $j=0,1$ represents the feature index number.
</div>

At each iteration j, <mark>one should simultaneously update</mark> the parameters $\theta_1, \theta_2,...,\theta_n$. Updating a specific parameter prior to calculating another one on the $j^{(th)}$ iteration would yield to a wrong implementation.

![Gradient descent 2]({{img-url}}/gradient-descent-2.png){:.no-border}

### Gradient descent intuition 1 (one variable)

In this video we explored the scenario where we used one parameter $\theta_1$ and plotted its cost function to implement a gradient descent. Our formula for a single parameter was :

<div class="p-mark">
Repeat until convergence:

$$
\theta_1:=\theta_1-\alpha \frac{d}{d\theta_1} J(\theta_1)
$$
</div>

Regardless of the slope's sign for $\frac{d}{d\theta_1} J(\theta_1)$, $\theta_1$ eventually converges to its minimum value. The following graph shows that when the slope is negative, the value of $\theta_1$ increases and when it is positive, the value of $\theta_1$ decreases.

![Gradient descent 2-1]({{img-url}}/gradient-descent-2-1.png){:.no-border}

On a side note, we should adjust our parameter $\alpha$ to ensure that the gradient descent algorithm converges in a reasonable time. Failure to converge or too much time to obtain the minimum value imply that our step size is wrong.

![Gradient descent 2-2]({{img-url}}/gradient-descent-2-2.png){:.no-border}

How does gradient descent converge with a <mark>fixed step size $\alpha$</mark>?
The intuition behind the convergence is that $\frac{d}{d\theta_1}$ approaches 0 as we approach the bottom of our convex function. At the minimum, the derivative will always be 0 and thus we get:

$$
\theta_1:=\theta_1-\alpha * 0
$$

![Gradient descent 2-3]({{img-url}}/gradient-descent-2-3.png){:.no-border}

### Gradient descent for linear regression

<div class="p-mark">
$J(\theta_0, \theta_1)$ in linear regression is always in "bowl shape" function or **convex function**.
</div>

When specifically applied to the case of linear regression, a new form of the gradient descent equation can be derived. We can substitute our actual cost function and our actual hypothesis function and modify the equation to :

<div class="p-mark">	
$$
\begin{align*} \text{repeat until convergence: } \lbrace & \newline \theta_0 := & \theta_0 - \alpha \frac{1}{m} \sum\limits_{i=1}^{m}(h_\theta(x_{i}) - y_{i}) \newline \theta_1 := & \theta_1 - \alpha \frac{1}{m} \sum\limits_{i=1}^{m}\left((h_\theta(x_{i}) - y_{i}) x_{i}\right) \newline \rbrace& \end{align*}
$$
</div>

where m is the size of the training set, $\theta_0$ a constant that will be changing simultaneously with $\theta_1$ and $(x_i,y_i)$ are values of the given training set (data).

Note that we have separated out the two cases for $\theta_j$ into separate equations for $\theta_0$ and $\theta_1$; and that for $\theta_1$ we are multiplying $x_{i}$ at the end due to the derivative. The following is a derivation of $\frac {\partial}{\partial \theta_j}J(\theta)$ for a single example :

$$
\begin{align}
\dfrac{\partial}{\partial\theta_j} J(\theta)
&= \dfrac{\partial}{\partial\theta_j} \dfrac{1}{2} (h_{\theta}(x)-y)^2 \\
&= (h_{\theta}(x)-y) \dfrac{\partial}{\partial\theta_j} \left( \sum_{i=0}^n \theta_ix_i - y \right)\\
&= (h_{\theta}(x)-y) x_j.
\end{align}
$$

The point of all this is that if we start with a guess for our hypothesis and then repeatedly apply these gradient descent equations, our hypothesis will become more and more accurate.

So, this is simply gradient descent on the original cost function J. This method looks at every example in the entire training set on every step, and is called **batch gradient descent**. Note that, while gradient descent can be susceptible to local minima in general, <mark>the optimization problem we have posed here for linear regression has only one global, and no other local, optima</mark>; thus **gradient descent always converges** (assuming the learning rate $\alpha$ is not too large) to the global minimum. Indeed, **J is a convex quadratic function**. Here is an example of gradient descent as it is run to minimize a quadratic function.

![Gradient descent 3-1]({{img-url}}/gradient-descent-3-1.png){:.no-border}

The ellipses shown above are the contours of a quadratic function. Also shown is the trajectory taken by gradient descent, which was initialized at (48,30). The x’s in the figure (joined by straight lines) mark the successive values of θ that gradient descent went through as it converged to its minimum.

## Linear Algebra review

{% include more.html content="[Download Lecture 3](/files/ML-coursera/Lecture3.pdf)." %}

Refer to [note of Linear Algebra]({{site.baseurl}}/linear-algebra-1). For LA in this course of Ng, it's very simple, I knew all about this to I don't give any note here.
​	