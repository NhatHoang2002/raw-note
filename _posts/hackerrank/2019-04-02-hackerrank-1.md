---
title: "Hackerrank 1: 10 days of statistics"
categories: [python,math]
tags: [hackerrank, statistics, python]
math: 1
toc: 1
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
b(x,n,p) = \binom {n}{k}\times p^x \times q^{1-x}
$$

- **Cumulative Probability** (<mark>CDF</mark>): $F_X(x) = P(X\le x)$ and $P(a<X\le b) = F_X(b)-F_X(a)$.



