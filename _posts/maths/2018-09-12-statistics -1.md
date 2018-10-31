---
title: Statistics 1
categories: [math]
tags: [machine learning, statistics, data, R]
math: 1
toc: 1
date: 2018-10-30
---

{% assign img-url = '/images/posts/math/statistics' %}

This note is only used for my learning statistics for data science. It's not a theoretical aspect, it's only statistics for data scientist.

(Maybe I starts to note this note while reading book *Introduction to statistical learning* by Gareth James)

{% include toc.html %}

## Documentation and books

- [Free Must Read Books on Statistics & Mathematics for Data Science](https://www.analyticsvidhya.com/blog/2016/02/free-read-books-statistics-mathematics-data-science/)
	- **Introduction to Statistical Learning** (downloaded) : this book uses R but there is code in Python [here](https://github.com/tdpetrou/Machine-Learning-Books-With-Python/tree/master/Introduction%20to%20Statistical%20Learning) or [here](https://github.com/JWarmenhoven/ISLR-python). See [**my note**](/tags#isl_cap).
	- **Elements of Statistical Learning** (downloaded)
	- **Think Stats** (downloaded)
- **Data Science from Scratch First Principles with Python** (downloaded)

## Concepts

- [What is Expected Value?](https://towardsdatascience.com/what-is-expected-value-4815bdbd84de)
- 

## 10 days of statistics on HackerRank

{% include more.html content="[Goto this Chalenge](https://www.hackerrank.com/domains/tutorials/10-days-of-statistics)." %}

- **Mean, Median, Mod**:
	- `mean` = mean value $\frac{1}{n}\sum_i x_i$
	- `median` = the number at the center, if the number of elements are odd, it's the center number, if even, it's the mean of two center elements.
	- `mod` = number(s) with the most number of appearances.

- **Quartile** of an <mark>ordered</mark> data set are the 3 points that split the data set into 4 groups. 
	- $Q_1$: the **middle** number between the **smallest number** in a data set and its **median**
	- $Q_2$: the **median** ($50^{th}$ percentile) of the data set
	- $Q_3$: the **middle** number between a data set's **median** and its **largest number**
	- **Algorithm**:
		- If the number of elements is odd, don't include the median for each half when seeking $Q_1, Q_2$
		- If the number of elements is even, just devide into 2 halves.
		- $Q_1$ is the median of first half, $Q_2$ is the median of second half.

- Find `median` without `numpy`

	~~~ python
def find_median(lst):
		len_lst = len(lst)
		if len_lst % 2 == 1:
				return lst[len_lst//2]
		else:
				return (lst[len_lst//2-1] + lst[len_lst//2])/2
	~~~

### Binomial distribution

A binomial experiment (or Bernoulli trial) is a statistical experiment that has the following properties: 

- The experiment consists of  repeated trials.
- The trials are independent.
- The outcome of each trial is either success ($s$) or failure ($f$).

### Bernoulli Random Variable and Distribution

Check for short resume [here](https://www.hackerrank.com/challenges/s10-binomial-distribution-1/tutorial).

## Python codes notes

Find **mean**, **median** and **mode**

~~~ python
import numpy as np
from scipy import stats 

print(np.mean(<list>))
print(np.median(<list>))
print(int(stats.mode(<list>)[0]))
~~~