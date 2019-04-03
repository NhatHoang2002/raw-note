---
title: "Hackerrank 1: 10 days of statistics"
categories: [python,math]
tags: [hackerrank, statistics, python]
math: 1
toc: 1
date: 2019-04-03
---

{% assign img-url = '/images/posts/hackerrank' %}

This note is only used for learning on Hackerrank - 10 days of Statistics.

{% include toc.html %}

{% include more.html content="[Goto this Chalenge](https://www.hackerrank.com/domains/tutorials/10-days-of-statistics)." %}

## Day 0 : Mean, Median, Mod, Weighted mean

- **mean** = mean value $\frac{1}{n}\sum_i x_i$
- **median** = the number at the center, if the number of elements are odd, it's the center number, if even, it's the mean of two center elements.
- **mod** = number(s) with the most number of appearances.
- Given a set of numbers, X, and corresponding set of weights, W, the **weighted mean** is calculated as follows
	$$
	m_w = \dfrac{\Sigma (x_i\times w_i)}{\Sigma w_i}
	$$
- Find `median` without `numpy`

	~~~ python
	def find_median(lst):
		len_lst = len(lst)
		if len_lst % 2 == 1:
				return lst[len_lst//2]
		else:
				return (lst[len_lst//2-1] + lst[len_lst//2])/2
	~~~
- With **numpy**
	~~~ python
	import numpy as np
	from scipy import stats 
	
	print(np.mean(<list>))
	print(np.median(<list>))
	print(int(stats.mode(<list>)[0]))
	~~~

## Day 1 : Quartiles, Interquartile Range, Standard Deviation

- **Quartile** of an <mark>ordered</mark> data set are the 3 points that split the data set into 4 groups. 
	- $Q_1$: the **middle** number between the **smallest number** in a data set and its **median**
	- $Q_2$: the **median** ($50^{th}$ percentile) of the data set
	- $Q_3$: the **middle** number between a data set's **median** and its **largest number**
	- **Algorithm**:
		- If the number of elements is odd, don't include the median for each half when seeking $Q_1, Q_2$
		- If the number of elements is even, just devide into 2 halves.
		- $Q_1$ is the median of first half, $Q_2$ is the median of second half.
- **Get the input**:
	~~~ python
	size = int(input())
	numbers = list(map(int, input().split()))
	~~~
- The **interquartile range** of an array is the difference between its first (Q1) and third (Q3) quartiles
- **Output** (0.9): `print("{:.1f}".format(Q3-Q1))`
- **Expected value** $\mu$ = mean of discrete random variable X.
- **Variance** $\sigma^2$: $\sigma^2 = \dfrac{\Sigma (x_i-\mu)}{n}$

- **Standard deviation** $\sigma$: $\sigma^2 = \sqrt{\dfrac{\Sigma (x_i-\mu)}{n}}$

- Use `sqrt`: `import math as m`

## Day 2 : Basic probability

- $P(A) = \dfrac{\text{favorable outcomes}}{\text{total outcomes}}$
- $0\le P(A)\le 1$
- $P(A^C) = 1-P(A)$
- **mutually exclusive** or **disjoint**: $A\cap B=\emptyset, P(A\cap B)=0$
- A,B are disjoint (mutually exclusive): $P(A\cup B) = P(A) + P(B)$
- A,B are **independent**: $P(A \cap B) = P(A)\times P(B)$
- Genreal: $\vert A\cup B\vert = \vert A\vert + \vert B\vert -\vert A\cap B\vert$

## Day 3 : Conditional probability

- A, B are considered to be independent if event: $P(B\vert A) = P(B)$
- $P(A\cap B) = P(B\vert A)\times P(A)$
- $P(B\vert A) = \dfrac{P(A\cap B)}{P(A)}$
- **Bayes' theorem**: 

$$
P(A\vert B) = \dfrac{P(B\vert A)\times P(A)}{P(B)} 
= \dfrac{P(B\vert A)\times P(A)}{P(B\vert A)\times P(A) + P(B\vert A^c)\times P(A^c)} 
$$

- **Permutations** (hoán vị): take r-element permutation from n elements (don't care about order): $nPr = \dfrac{n!}{(n-r)!}$
- **Combinations** (chỉnh hợp): take r-element from n elements (care about order): $nCr = \dfrac{nPr}{r!} = \dfrac{n!}{r!(n-r)!}$

## Day 4 : Binomial distribution

- [Tutorial link.](https://www.hackerrank.com/challenges/s10-binomial-distribution-1/tutorial)
- **Random variable** X:is the real value function $X: S\to R$ in which there is an event for each interval $I\subseteq R$ 
- A **binomial experiment** (or **Bernoulli trial**) is a statistical experiment that has the following properties: 
	- The experiment consists of  repeated trials.
	- The trials are independent.
	- The outcome of each trial is either success ($s$) or failure ($f$).
- **Bernoulli Random Variable and Distribution**: The sample space of a binomial experiment only contains two points, s and f. We define a Bernoulli random variable to be the random variable defined by $X(s)=1$ and $X(f)=0$. If we consider the probability of success to be p and the probability of failure to be q (where $q=1-p$), then the probability mass function (<mark>PMF</mark>) of  is:

$$
p(x) = \begin{cases}
1-p=q \quad if\, x=0,\\
p \quad if\, x=1\\
0 \quad otherwise
\end{cases}
$$

or

$$
f(x) = p^x(1-p)^{1-x},\quad for\, x\in \{0,1\}.
$$

- **[Binomial distribution](https://en.wikipedia.org/wiki/Binomial_distribution)**: is the binomial probability, meaning the probability of having exactly x successes out of n trials. 
	- The number of successes is x.
	- The total number of trials is n.
	- The probability of success of 1 trial is p.
	- The probability of failure of 1 trial q, where q=1-p.


$$
b(x,n,p) = \binom {n}{x}\times p^x \times q^{1-x}
$$

- **Cumulative Probability** (<mark>CDF</mark>): $F_X(x) = P(X\le x)$ and $P(a<X\le b) = F_X(b)-F_X(a)$.

## Day 4 : Geometric Distribution

- **Negative Binomial Experiment**: A negative binomial experiment is a statistical experiment that has the following properties:
	- The experiment consists of n repeated trials.
	- The trials are independent.
	- The outcome of each trial is either success (s) or failure (f). 
	- P(s) is the same for every trial.
	- The experiment continues until x successes are observed. 
- If x is the number of experiments until the xth success occurs, then X is a discrete random variable called **a negative binomial**. 

$$
b^{\ast}(x,n,p) = \binom {n-1}{x-1}\times p^x \times q^{1-x}
$$

- The number of successes to be observed is x.
- The total number of trials is n.
- The probability of success of 1 trial is p.
- The probability of failure of 1 trial q, where q=1-p.
- $b^{\ast}(x,n,p)$ is the negative binomial probability, meaning the probability of having x-1 successes after n-1 trials and having x successes after n trials.

- **Geometric Distribution**: The geometric distribution is a special case of the negative binomial distribution that deals with the number of Bernoulli trials required to get a success (i.e., *counting the number of failures before the first success*). Recall that X is the number of successes in n independent Bernoulli trials, so for each i (where $1\le i \le n$):

$$
X_i = \begin{cases}
1 \quad \text{if the ith trial is a success}\\
0 \quad \text{otherwise}
\end{cases}
$$

- The geometric distribution is a negative binomial distribution where the number of successes is 1. We express this with the following formula:

$$
g(n,p) = q^{n-1}\times p.
$$

## Day 5 : Poisson Distribution

- A **Poisson experiment** is a statistical experiment that has the following properties:
	- The outcome of each trial is either success or failure.
	- The average number of successes ($\lambda$) that occurs in a specified region is known.
	- The probability that a success will occur is proportional to the size of the region.
	- The probability that a success will occur in an extremely small region is virtually zero.
- A Poisson random variable is the number of successes that result from a Poisson experiment. The probability distribution of a Poisson random variable is called a **Poisson distribution**: 

$$
P(k, \lambda) = \dfrac{\lambda^k e^{-\lambda}}{k!}
$$

- $e=2.71828$
- $\lambda$ is the average number of successes that occur in a specified region.
- k is the actual number of successes that occur in a specified region.
- $P(k,\lambda)$ is the Poisson probability, which is the probability of getting exactly k successes when the average number of successes is $\lambda$. 
- Check examples & special case [here](https://www.hackerrank.com/challenges/s10-poisson-distribution-1/tutorial).
- **Special case**: X has Poisson Distribution, $E[X] = \lambda = Var(X), Var(X) = E[X^2] - (E[X])^2$ 

## Day 5 : Normal Distribution

- The **probability density of normal distribution** is:

$$
N(\mu,\sigma^2) = \dfrac{1}{\sigma\sqrt{2\pi}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}
$$

- $\mu$ is the mean (or expectation) of the distribution. It is also equal to median and mode of the distribution.
- $\sigma^2$ is the variance.
- $\sigma$ is the standard deviation. 
- In python, we can use `numpy.random.normal` ([ref](https://docs.scipy.org/doc/numpy/reference/generated/numpy.random.normal.html))
- If $\mu=0, \sigma=1$ then the normal distribution is known as **standard normal distribution** 

$$
\phi(x) = \dfrac{e^{-\frac{x^2}{2}}}{\sqrt{2\pi}}
$$

- Every normal distribution can be represented as standard normal distribution:

$$
N(\mu,\sigma^2) = \frac{1}{\sigma}\phi(\frac{x-\mu}{\sigma})
$$

- Consider a real-valued random variable, X. The **cumulative distribution function** of X (or just the **distribution function** of X) evaluated at x is the probability that X will take a value less than or equal to x:

$$
F_X(x) = P(X\le x) \\
P(a\le X\le b) = P(a<X<b) = F_X(b) - F_X(a)
$$

- The **cumulative distribution function** for a function with normal distribution is (erf = error function):

$$
\Phi(x) = \frac{1}{2}(1+\text{erf}(\frac{x-\mu}{\sigma\sqrt{2}})) \\
\text{erf}(z) = \frac{2}{\sqrt{\pi}}\int_0^z e^{-x^2}dx
$$

- In python, we can use [`math.erf` function](https://docs.python.org/3.5/library/math.html#math.erf).