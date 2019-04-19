---
layout: post
title: "IBM Data Course 4: Python for Data Science"
categories: [data]
tags: [data, ibm data, python]
toc: 1
comment: 1
---

{% assign img-url = '/images/posts/data/ibm' %}

This note was first taken when I learnt the [IBM Data Professional Certificate course](https://www.coursera.org/specializations/ibm-data-science-professional-certificate) on Coursera.

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Course 3](/ibm-data-professional-certificate-2).
</span>
</div>

{% include more.html content="[Go to Course 5](/ibm-data-professional-certificate-4)." %}

{% include toc.html %}

## Week 1: Python Basics

- **Types**
	- Types: `int`, `float`, `str`, `bool`
	- Check the type: `type(11)`
	- Boolean: `True`, `False`
	- `int(12.8)` or `int(12.3)` will return `12`
- **Expressions and Variables**
	- Operators: `+,-*,/`.
	- `/` returns a `float`
	- `//` returns a `int`
	- `11//5` returns `1`
- **String**
	- Think a string as an order sequence, `a = 'dinhanhthi'`
	- Can use indexes (start from 0) to consider a character in a string, `a[0]` returns `d`
	- Indexes can be a negative number, `a[-1]` returns `i`
	- Index can be a range, `a[1:3]` returns `in` (don't consider the last number in the range)
	- **stride**: `a[::2]` returns `dnahh`
	- If `b='123456'` then `b[1::2]` returns `'246'`
	- lenght of string: `len(a)` returns `10`
	- combine 2 string, use `+`
	- we also can use multiply on string: `a*3` returns `dinhanhthidinhanhthidinhanhthi`
	- **string is immutable**, we **cannot** do this `a[0]=s`
	- `\n` returns new line in string
	- `'t` returns a tab in string
	- `\\` returns `\`
	- print everything: `print(r'dinh \n anh')` returns `dinh \n anh`
- **String methods**
	- `a.upper()` returns `DINHANHTHI`
	- `a.replace('dinh','tran')` returns `trananhthi`
	- Find a substring: `a.find(anh)` returns `4`


## Week 2 : Python Data Structures

- **Tuples**
	- Ordered sequence, `a = (1,'thi',3.2,4,5)`
	- `type(a)` returns `tuple`
	- `a[1]` returns `'thi'`
	- `a[-1]` returns `5`
	- `b = a + (6,'dinh')` returns `(1,'thi',2,3.2,4,5,6,'dinh')`
	- Can apply slicing, `a[1:3]` returns `('thi',3.2)`
	- `len(a)` returns 5
	- Tuples is **immutable** (we can't change them)
	- `a=(1,3,2)`, `b=sorted(a)` returns a list `[1,2,3]`
	- if `a=(1,'thi')`, we cannot apply `sorted`
	- tuple is **nesting**, `c = (1,2,(3,4),'thi')`
	- `c[2][1]` returns `4`
- **Lists**
	- Ordered sequence, `a = ['thi',2,3,4]`
	- List **is mutable**, `a[1]=5` then a takes `['thi',5,3,4]`
	- **Nesting**, `b = [[1,2],'thi',3.2]`
	- `a + b` returns `['thi',2,3,4,[1,2],'thi',3.2]`
	- `a.extend([5,6])` returns `['thi',2,3,4,5,6]`
	- `a.append([5,6])` returns `['thi',2,3,4,[5,6]]` (only 1 element to be appended)
	- **Every time we apply methods, list changes**
	- Remove some element: `del(a[0])` and then a takes `[2,3,4]`
	- `'a,b,c,d'.split(",")` returns `['a','b','c','d']`
	- `d='[1,2]'`, `e=d`. If d changes, e changes too. They refer to the same list.
	- **Clone**: `e=d[:]`. e and d **are different**
	- **Get helps**: `help(a)`
- **Dictionaries**
	- Type of collections in python, `a = {'key1':1, 'key2':[1,2]}`
	- `a['key1']` returns `1`
	- Add new entry: `a['key3'] = (1,2)`
	- Delete: `del(a['key2'])`
	- Check: `'key3' in a` returns `True`
	- `a.keys()` returns `['key1','key2','key3']`
	- The same: `a.values()`
	- `a = {'key':1, 'key':2}` then a returns `{'key':2}`
- **Sets**
	- A type of collections, `a = {'thi',2,3}`
	- They are **unordered**.
	- **Have unique element**
	- `b = {1,2,1}` then b takes `{1,2}`
	- `set(<list>)` returns a set. **Duplicated elements are removed** to keep only one.
	- `a.add(5)`
	- `a.remove('thi')`
	- Check: `2 in a` returns `True`
	- Intersect between 2 sets: `c = a & b`
	- Union: `c = a.union(b)`
	- Check the subset? `a.issubset(b)` to check if a is a subset of b?

## Week 3: Python Programming Fundamentals

- **If**
	- Comparison Operators: `a==b`, `>, <, >=, <=, !=`
	- Logic operators: `not(a)`, `a or b`, `a and b`

		~~~ python
		if (conditions):
			statements
		
		if (conditions):
			statements
		else:
			statements
		
		if (conditions):
			statements
		elif (conditions):
			statements
		else:
			statements
		~~~

- **For**
	- `range(5)` returns a list `[0,1,2,3,4]`
	- `range(10,15)` returns `[10,11,12,13,14]`

		~~~ python
		for i in range(5):
			statements
		
		a = ['1','2','3']
		for i in a:
			statements
		
		for idx, val in a:
			statements
			# idx: index of elements in a
			# val: values of element in a
		~~~
	
- **While**

	~~~ python
	while (conditions):
		statements
	~~~

- **Functions**
	- `sorted(a)` returns **new** sorted list or tuple but a doesn't change
	- `a.sort()` makes a change
	- Global var can be used in the local function but not inverse

		~~~ python
		def name(variables):
			statements
			return value
		
		def MJ():
			print("Micheal Jackson")
		
		def NoWork():
			pass // return None
		
		~~~

- **Objects and Classes**
	- An object has following 
		- type
		- an internal data representation (a blueprint)
		- methods
	- An object is an instance of particular type
	- `type(<object>)` finds the type of an object
	- class = type's method = all functions that class/type provides
	- Use `dir(<nameOfObject>)` to check all methods inside a class/object

		~~~ python
		class Circle(onject):
			def __init__(self, radius, color):
				self.radius = radius
				self.color = color
		
			def add_radius(self,r):
				self.radius = self.radius + r
		
		RedCircle = Circle(10,'red')
		RedCircle.radius // returns 10
		
		RedCircle.add_radius(8) // returns 18
		~~~


## Week 4: Working with Data in Python

- **Reading a file with open**
	- `file1 = open(<path>,'r')` where `w` (writing), `r` (reading), `a` (appending)
	- `file1` is file object
	- `file1.name` for name of file, `file1.mode` to see `r`
	- Close the file: `file1.close()`
	- `file1.closed` check if file is closed or not?
	- Using `with` to automatically close the file after using it.
		~~~ python
		with open("filename.txt","r") as file1:
			file_stuff = file1.read()
			print(file_stuff)
		~~~
	- `file1.readlines()` returns a list, each element as a line in file.
	- `file1.readline()` return each line.
- **Writing files with Open**
	- `file1 = open(<path>,'w')`
		~~~ python
		with open("filename.txt","w") as file1:
			file1.write("line 1")
		~~~
	- We can use mode `"a"` to add new line to the file 
		~~~ python
		with open("filename.txt","a") as file1:
			file1.write("line 2")
		~~~
	- We can copy a file as follows

		~~~ python
		with open("filename1.txt","r") as file1:
			with open("filename2.txt","w") as file2:
				for line in file1:
					file2.write(line)
		~~~
- **Loading data with Pandas**
	- `import pandas as pd`
	- `df = pd.read_csv(<csv_path>)`
	- `df.head()` returns first 5 lines in dataframe
	- `df.read_excel(<excel_path>)`
	- Create (by hand) a df as a dictionary where keys as a columns, each value is a list stading for a row.
	- `x = df[['lenght']]` create a new df consisting 1 column.
	- or multiple columns: `x = df[['col1','col2','col3']]`
	- `df.ix[0,0]` consider the element at row 0 and column 0
	- `df.ix[1,'artist']` consider the 1st row and column named "artist"
	- `df.ix[1:3,2:1]`
	- `df.ix[1:3,'artist':'released']`
- **Working with and saving data in Pandas**
	- `df['released'].unique()` returns a column containing unique values.
	- `df[df['released']>=1980]` returns a df whose column "released" has value >= 1980
	- Save df: `df1.to_csv(<filename.csv>)`
- **One dimensional Numpy**
	- `import numpy as np`
	- `a = np.array([0,1,2,3,4])`
	- `a[2]` returns 2
	- `type(a)` returns **np.ndarray**
	- `a.dtype` returns `dtype('int64')`
	- `a.size` returns number of elements in the array
	- `a.ndim` returns the number of array's dimension (1)
	- `a.shape` returns the shape of the array (5,)
	- Change value of each element in the array: `a[0] = 100`
	- `d = a[1:3]` returns `d=array([1,2])`
	- `a + b` returns elementwise adding.
	- `a*2`: each element multiplies by 2
	- `a*b`: multiply elementwise
	- `np.dot(a,b)`: dot product
	- `a+1`: add 1 to each element
	- `a.mean()`: find the mean of all elements in the array
	- `a.max()`: largest value in the array 
	- `np.pi, np.sin()`
	- `np.linear(-2,2,num-5)`: creates an array containing 5 elemnets from -2 to 2
	- **Plot**: `import matplotlib.pyplot as plt`
	- `plt.plot(x,y)` where x,y are 2 arrays
- **Two Dimensional Numpy**:
	- `a = [[1,2],[3,4]]` and then cast the list `A = np.array(a)`
	- `A.ndim` returns 2 : the number of nested lists
	- `A.shape` returns (2,2)
	- `A.size` returns 4
	- `A[0][1]`, `A[0:2,1]`


## Week 5: Fake Album Cover Game

- **Web scraping** or **harvesting data** involves extracting data from websites.
- `from IPython.display import Image as IPythonImage` and then use `IPythonImage(filename='sample-out.png')` to display image in python notebook.
- Random Wiki post: [https://en.wikipedia.org/wiki/Special:Random](https://en.wikipedia.org/wiki/Special:Random)

~~~ python
import requests
wikipedia_link='https://en.wikipedia.org/wiki/Special:Random'
raw_random_wikipedia_page = requests.get(wikipedia_link)
page = raw_random_wikipedia_page.text // page source as a string "page"
print(page)
~~~