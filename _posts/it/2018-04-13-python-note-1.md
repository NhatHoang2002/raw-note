---
title: Python note 1
categories:
  - it
tags: ["python","tự học","lập trìnnh"]
maths: 1
toc: 1
date: 2018-08-18
---

{% include toc.html %}

<div style="margin-top: -1rem;"></div>


## Tài liệu

- **Dùng để tra cứu**
	- [programiz.com](https://www.programiz.com) : **nên dùng để tra**
	- [Python trên w3school](https://www.w3schools.com/python) : nên dùng để xem và check ví dụ (không đầy đủ các method)
	- [Python 3](https://www.tutorialspoint.com/python3/index.htm) on **tutorialspoint** : nên dùng để xem danh sách hết các method trong mỗi objects.
	- Python documentation: [http://devdocs.io/python~3.6/](http://devdocs.io/python~3.6/)
  		- [Official docs](https://docs.python.org/3/) : chỉ dùng khi tra từ google
	- **App mobile** (dành để đọc ref): [Python Reference](https://itunes.apple.com/us/app/python-reference/id1386866064?mt=8) của Wenhuan Li
- **Course, learning**
	- Course on Pluralsight: [Python fundamentals by Austin Bingham and Robert Smallshire](https://app.pluralsight.com/library/courses/python-fundamentals/table-of-contents)
	- Video bài giảng của [Corey Schafer](https://www.youtube.com/user/schafer5/playlists) (anh Việt recommend)
	- [How to think like a computer scientist?](http://openbookproject.net/thinkcs/python/english3e/index.html) : sách được thể hiện dưới dạng html
	- [RealPython](https://realpython.com/start-here/)
- **Exercise, practice**
	- [Exercism](https://exercism.io/my/tracks/python) : học bằng bài tập, có nhiều ngôn ngữ khác nữa, free 100% (xem thêm [note riêng cho nó](/python-exercism-1))
	- [Python exercises](https://www.w3resource.com/python-exercises)
- **Others**:
	- [Newsletter for python](https://www.pythonweekly.com/): docs, jobs, news,....
	- [Insert Datacamp interative Python inside web/blog](https://github.com/datacamp/datacamp-light) (also for R)



## Install

- Có thể cài mọi thứ thông qua [Anaconda](https://anaconda.com), tuy nhiên trên Windows vẫn chưa tự nhận thông qua Command Prompt.
- Trên Linux hay Mac thì python tự nhận trong terminal, windows thì cần làm thêm các bước bên dưới.



### exercism

- Cái này dành để học trên trang web [exercism.io](https://exercism.io/tracks/python/tests)
- Cài **pytest**: `pip3 install pytest pytest-cache`

Install **CLI**

1. Download [latest cli](https://github.com/exercism/cli/releases)
2. Run `start "" "%LOCALAPPDATA%\Microsoft\WindowsApps"` in cmd
3. Move all extracted files/folder from step 1 to folder *WindowsApps*
4. Verify xem thành công không bằng cách gõ vào cmd `exercism`
5. Install thành công
6. Configure CLI: `exercism configure --token=c2562d83-65ea-4176-ab80-ff058b111cf9`



### Làm cho Windows "nhận"

- Nếu tự cài [Python](https://www.python.org/), cần add nó vào PATH của hệ thống Windows.
- Cũng phải cần cài path của Anaconda vào PATH của Windows.

1. Start > gõ "Path", mở *Edit the system enviroment variables*
2. Enviroment Variables > User variables for ... > click double vào **path**
3. Click double vào hàng trống cuối cùng trong list > Dán đường dẫn Anaconda vào
	1. Để có thể tìm đường dẫn Anaconda, nhấn Start > gõ "Anaconda" > chuột phải > Open file location 
	2. Nó mở ra cửa sổ chứa mấy file shortcut > chuột phải lần nữa vào Anaconda > Optn file location > nó sẽ mở đường dẫn của Anaconda, thông thường sẽ là **C:\ProgramData\Anaconda3**
3. Lưu ý, lưu thư mục chứa mấy file python.exe chứ không có lưu cả file đó.
4. Sau khi add vào PATH, cần phải restart lại [cmder](http://cmder.net/) (command prompt thì khỏi)



### Jupyter notebook

- [Cái này](http://jupyter.org/index.html) có sẵn nếu đã cài Anaconda.
- Trên **Windows**, không thể chạy nó bằng dòng lệnh `jupyter notebook` như các [trang hướng dẫn](https://jupyter.readthedocs.io/en/latest/running.html) được!
- Mà phải chạy bằng `python -m notebook` (chỉ có tác dụng sau khi đã add python path vào PATH của hệ thống như ở trên hướng dẫn)
- Cũng có thể chạy file Jupyter Notebook có sẵn nhưng đường dẫn mặc định sau khi chạy xong (localhost:8888) không theo ý mình (ngoài /Home/), do đó, cần dùng [cmder](http://cmder.net/) (or command prompt) `cd` đến thư mục cần làm "host", sau đó chạy dòng lệnh `python -m notebook` như ở trên hướng dẫn.


### Install package with `pip`

- Trên Windows, thường nó sẽ hiện *'pip' is not recognized as an internal....*, lý do là bởi cmd chưa nhận ra *pip.exe* đang nằm ở đâu, hãy *add nó vào PATH của hệ thống* giống như hướng dẫn ở mục **Làm cho Windows "nhận"**
- Nếu cài Anaconda, đường dẫn của pip là **C:\ProgramData\Anaconda3\Scripts**, nếu cài python riêng lẻ, đường dẫn của pip nằm ở trong thư mục **Scripts** nơi chứa python.exe.
- **Update pip**: `python -m pip install --upgrade pip` (phải chạy cmd/cmder bằng quyền admin trước khi cài)
- **Error**
	- *distributed 1.21.8 requires msgpack, which is not installed.*: `pip install msgpack`
- Other, read [this](https://pip.pypa.io/en/stable/installing/) to install pip.



## Linh tinh

- `y=x`, nếu `y` change thì `x` cũng change luôn. Thay vào đó, dùng `y=list(x)` hoặc `y=x[:]`

- [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop) (read-eval-print-loop) : là môi trường gõ lệnh đơn lẻ, có thể dùng [reple.it](http://repl.it)

  - Exit: Ctrl+Z (Windows), Ctrl+D (Linux, Mac)
- **Clear**:
	- `del <biến>` : giống `clear` trong matlab, không cần confirm
	- `%reset` : xóa hết biến trong workspace hiện tại (giống `clear all` trong matlab). Nếu muốn clear 1 biến cụ thể, dùng `%reset_selective <biến>`. Cái này **cần confirm**
		- Nếu không muốn thấy confirm, dùng `%reset -f`


## IPython & Spyder

- `clear` giống `clc` (clear hết trên khung màn hình)
- `%reset` : xóa hết biến trong workspace hiện tại (giống `clear all` trong matlab). Nếu muốn clear 1 biến cụ thể, dùng `%reset_selective <biến>`
- Chọn lệnh xong nhấn **Ctrl+Enter** để chạy code trong **Spyder**
- Chọn command, sau đó nhấn **Ctrl+I** để xem help về command đó trong **Spyder**.


## Zen of python

### General notes

- không dùng `;` chỉ dùng thụt đầu dòng. Nếu muốn 2 lệnh trên 1 dòng thì cách nhau bởi `;`
- Tab size trong Python là 4 spaces
- Có thể break lines bình thường trong python, không cần dùng thêm ký hiệu gì (nhớ thụt đầu dòng vao) HOẶC dùng dấu `\`

  ~~~ python
  a = '1' + '2' + '3' + \
      '4' + '5'
  # or
  a = ('1' + '2' + '3' +
      '4' + '5')
  ~~~

- Có thể dùng: `a = 1_000_000` (from python 3.6)
- [PEP](https://www.python.org/dev/peps/) (Python Enhancement Proposals)

  - [PEP 8](https://www.python.org/dev/peps/pep-0008/) - Python style guide
  - [PEP 20](https://www.python.org/dev/peps/pep-0020/) - The Zen of Python.



### Comments

- Using `#` on each line
- Multi lines dùng `"""` ở đầu và cuối, lưu ý, cái này cũng dùng để docstring, tức khi người dùng `help(ten_function)` thì mấy cái nằm trong đây sẽ được show ra. Ví dụ

	~~~ python
	def reverse(text):
	    """Reverse a text.
	    Input the text
		Return text reversed
	    """
		return text[::-1]
	~~~


## Input and Output

- get input from user and display

	~~~ python
	age = input("Your age? ") # python 3, raw_input for python 2
	print("Your age:",age) # don't need space after "age"
	~~~

	Lưu ý: Tất cả input get được đều ở dạng string, nếu muốn áp dụng toán vào thì cần chuyển về float (`float`) hoặc int (`int`)

- Xem thêm practice trên [Jupyter notebook](/jupyter/cs50.html)
- `print "Hello"` là của python 2, còn python 3 bắt buộc là `print("Hello")` ([cf](https://docs.python.org/3/whatsnew/3.0.html))
- `print()` print something, `read()` wait for user input something 

 

## Underscore

- Tham khảo [tại đây](https://hackernoon.com/understanding-the-underscore-of-python-309d1a029edc).
- When used in interpreter (nhớ lại kết quả trước đó, giống `ans` trong matlab)
- Cần ignore giá trị nào đó, giống `~` trong matlab.

	~~~ python
	x, _, y = (1, 2, 3) # x = 1, y = 3

	# ignore the index
	for _ in range(10)
		do_something(i)

	# Ignore a value of specific location
	for _, val in list_of_tuple:
	    do_something()
	~~~

- Để đặt tên, xem [PEP8](https://www.python.org/dev/peps/pep-0008/)
	- `__double_leading_and_trailing_underscore__`: "magic" objects or attributes that live in user-controlled namespaces. E.g. `__init__`, `__import__` or `__file__`. **Never invent such names**; only use them as documented.
	- `__double_leading_underscore`: when naming a class attribute, invokes name mangling (inside class `FooBar`, `__boo` becomes `_FooBar__boo`). Nghĩa là không gọi riêng cái biến với tên này được mà phải gọi lên tên của class.
	- `_single_leading_underscore`: weak "internal use" indicator. E.g. `from M import *` does not import objects whose name starts with an underscore. **biến private**



## Operators

- `+-*/` bình thường
- `//` chia số nguyên (kết quả là interger), còn `/` thì luôn ra `real`
- Relation: `==, !=, >, <, >=, <=`
- `i = i+1` $\Leftrightarrow$ `i += 1` and others
- **Ternary conditional operator**: `b = 100 if a>10 else 0` giống như `b = (a>10)?100:0` trong C++
- `from __future__ import division` đảm bảo phép chia `/` là chia số thực, nghĩa là `1/2` ra `0.5` chứ không phải ra `0` (cf. [PEP 238](https://www.python.org/dev/peps/pep-0238/)) $\Rightarrow$ **enabled by default in Python 3.x.**
- **Đổi biến** nhanh gọn: `a, b = b, a`


## Object and Class

- **Object comparison** ([cf](http://abregman.com/2016/11/29/python-objects-comparison/))
	- Below is an example of comparison

		~~~ python
		class Ball(object):
		    def __init__(self, color, size):
		        self.color = color
		        self.size = size
		
		ball1 = Ball('blue', 'small')
		ball2 = Ball('blue', 'small')
		
		print(ball1 == ball2) # Prints False!
		~~~

		Because python **compare the "id"** of `ball1` and `ball2` instead.
	
	- Do đó có các comparison *rich comparison methods* or *comparison magic methods* bên trong các class/object này để "định nghĩa" luôn *thế nào là bằng, lớn, nhỏ,...* giữa các object với nhau.

		~~~ python
		object.__lt__(self, other) # For x < y
		object.__le__(self, other) # For x <= y
		object.__eq__(self, other) # For x == y
		object.__ne__(self, other) # For x != y OR x <> y
		object.__gt__(self, other) # For x > y
		object.__ge__(self, other) # For x >= y
		~~~

	- Xem thêm trong [cf](http://abregman.com/2016/11/29/python-objects-comparison/).


## Condition, loops

- `if`, `for`, `while` ([cf](https://www.programiz.com/python-programming/if-elif-else))

	``` python
	# if
	if condition:
		comands
	elif
		commands
	else
		commands
	
	# while
	while condition:
	    commands
	# use `break` to break
	```

- Special operator (Ternary conditional operator): `a = 100 if b>1 else 5`



## Strings, bytes, list, dictionaries, sets

- index start in python 0 (mảng, table,...)
- Chú ý `x[1:3]` là lấy thằng thứ 2 và thứ 3 chứ ko có lấy thằng thứ 4. Kiểu nó sẽ lấy $1\le i < 3$.
- `"abc" + "xyz" = "abcxyz"`



## [Pandas](http://pandas.pydata.org/) package

*[pandas](https://pandas.pydata.org/)* is an open source, BSD-licensed library providing high-performance, easy-to-use data structures and data analysis tools for the [Python](https://www.python.org/) programming language

- `iloc`: select rows and columns by number (integer-location based indexing) [[xem thêm](https://www.shanelynn.ie/select-pandas-dataframe-rows-and-columns-using-iloc-loc-and-ix/)]
  ~~~ python
  # Rows:
  data.iloc[0] # first row of data frame (Aleshia Tomkiewicz) - Note a Series data type output.
  data.iloc[1] # second row of data frame (Evan Zigomalas)
  data.iloc[-1] # last row of data frame (Mi Richan)
  
  # Columns:
  data.iloc[:,0] # first column of data frame (first_name)
  data.iloc[:,1] # second column of data frame (last_name)
  data.iloc[:,-1] # last column of data frame (id)
  
  # Multiple row and column selections using iloc and DataFrame
  data.iloc[0:5] # first five rows of dataframe
  data.iloc[:, 0:2] # first two columns of data frame with all rows
  data.iloc[[0,3,6,24], [0,5,6]] # 1st, 4th, 7th, 25th row + 1st 6th 7th columns.
  data.iloc[0:5, 5:8] # first 5 rows and 5th, 6th, 7th columns of data frame (county -> phone1).
  ~~~
- `dataset.iloc[:,:-1].values`: chọn `values` của tất cả dòng (`:`) và tất cả cột trừ cột cuối (`:-1`)

## Import libraries

Ba hàm cơ bản khi học course ML A-Z

~~~ python
import numpy as np # "np là viết tắt, sau này dùng cho ngắn gọn
# library về toán

import matplotlib.pyplot as plt # có thể import sub lib bằng dấu "." như này
# vẽ charts, hình trong python thì dùng lib này

import pandas as pd
# lib dành cho import dataset và manage dataset
~~~

## Python with Visual Studio Code

**Quyết định chỉ dùng [Spyder](https://pythonhosted.org/spyder/installation.html)**

Trong đoạn code kêu dùng Python với Spyder nhưng mà nó không tương thích với HiDPI nên quyết định chọn VSC. Không chọn Pycharm nữa vì nó nặng quá, VSC nhẹ hơn rất nhiều và làm được cho mấy cái ngôn ngữ khác được.

- Cứ mở thử một file python .py lên, nếu chưa cài extension cho VSC thì nó sẽ hỏi, nhấn vào mà cài thôi, nó sẽ cài extension mang tên Python.
- Nó cũng hỏi và đề nghị cài thêm vài cái (quên tên), cứ cài thôi.
- Nó cũng kêu chọn Python Environments gì đó, trong đó có option chọn **Anaconda** thì cứ chọn thôi (thanh dưới cùng của cửa sổ).
- Xem thêm [ở đây](https://code.visualstudio.com/docs/languages/python) để biết về VSC + Python.

[Trong course](/machine-learning-1) có dùng Ipython để mỗi lần gõ lệnh xong, quét kéo thả vào là chạy, tuy nhiên không biết torng VSC làm ở đâu. Đọc thêm [bài viết này](https://donjayamanne.github.io/pythonVSCodeDocs/docs/jupyter_getting-started/).
