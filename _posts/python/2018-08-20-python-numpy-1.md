---
title: Python NumPy
categories: [ml, data]
tags: [python,numpy,data]
maths: 1
toc: 1
date: 2018-09-05
---

This post is for noting the `numpy` package in python. For other notes in python, see [this](/tags#python).

{% include toc.html %}

## Installation & doc

- `pip3 install numpy`
- [Documentation](https://docs.scipy.org/doc/numpy/) (use search function)

## Import

- `import numpy as np`

## Array

- Chia array element-wise cho nhau được. List không làm được điều này! Cái này giống `./` trong matlab.
- `[1,2] + [3,4]` gives `[1,2,3,4]` nhưng `numpy.array([1,2]) + numpy.array([3,4])` gives `array([4,6])`
- **Subsettings**

	~~~ python
	import numpy as np
	a = np.array([1,2,3])
	a[1] # 2
	a > 1 # array([False, True, True, dtype=bool])
	a[a > 1] # array([2,3])
	~~~

- numpy arrays **cannot** contain elements with **different types**
- 2d array

	~~~ python
	list = [[1,2,3,4,5],
			[6,7,8,9,0]]
	array = np.array(list)
	
	type(array) # gives numpy.ndarray which means N-dimensional array
	array.shape # gives (2,5) which means 2 rows and 5 columns
	
	array[0] # array([1,2,3,4,5])
	array[1][2] # 8
	array[1,2] # 8
	
	array[:, 1:3]
	array[1,:] # the same with array[1]
	~~~

- Nhân 2 array different size: `a` (3,3) * `b` (1,3) thì cột 1 a nhân với số đầu b hay cột đầu b và cứ thế.
- `numpy.mean(<array>)` gives $\dfrac{\Sigma x\_i}{N}$
- `numpy.median(<array>` gives số ở giữa (nếu số phần tử lẻ), trung bình cộng của 2 số ở giữa (nếu số phần tử chẵn)
- `numpy.std(<array>)` gives [standard deviation](https://www.mathsisfun.com/definitions/standard-deviation.html) (độ lệch chuẩn) which is a measure of how spread out numbers are.

## Comparison

- For example, we have an array `bmi`, then the following cannot be true

	~~~ python
	bmi > 21 and bmi < 22
	~~~
	
	One have to use
	
	~~~ python
	np.logical_and(bmi > 21, bmi < 22)
	~~~

- One can use `bmi[np.logical_and(bmi > 21)]` to get another array.

- See other logical operators in numpy [here](https://docs.scipy.org/doc/numpy/search.html?q=logical&check_keywords=yes&area=default).

## Random

- Number between $(0,1)$: `np.random.rand()`
- From a seed to generate the same random number: `np.random.seed(<number>)` and then run again the genration code.
- Print random integer numbers: `np.random.randint(0,2)` gives random of 0 and 1 (2 is not included).