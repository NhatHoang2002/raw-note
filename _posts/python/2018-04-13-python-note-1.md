---
title: Python 1
categories: it
tags: [python,coding]
maths: 1
toc: 1
date: 2018-08-24
datacamp: 1
comment: 1
---

Bài này giống như chương Introduction, những thứ cơ bản nhất về Python và chung nhất. Có những [note khác]({{site.baseurl}}/tags#python) dành cho từng mục đích sử dụng python/thư viện python khác nhau.

{% include toc.html %}


## Tài liệu

- **Dùng để tra cứu**
	- [programiz.com](https://www.programiz.com) : **nên dùng để tra**
	- [Python trên w3school](https://www.w3schools.com/python) : nên dùng để xem và check ví dụ (không đầy đủ các method)
	- [Python 3](https://www.tutorialspoint.com/python3/index.htm) on **tutorialspoint** : nên dùng để xem danh sách hết các method trong mỗi objects.
	- Python documentation: [http://devdocs.io/python~3.6/](http://devdocs.io/python~3.6/)
  		- [Official docs](https://docs.python.org/3/) : chỉ dùng khi tra từ google
	- **App mobile** (dành để đọc ref): [Python Reference](https://itunes.apple.com/us/app/python-reference/id1386866064?mt=8) của Wenhuan Li
- **Course, learning**
	- [Intro to python for data science](https://campus.datacamp.com/courses/intro-to-python-for-data-science/) : video rồi làm bài tập trực tiếp trên web, đang theo.
	- Course on Pluralsight: [Python fundamentals by Austin Bingham and Robert Smallshire](https://app.pluralsight.com/library/courses/python-fundamentals/table-of-contents) (chỉ video, không bài tập)
	- Video bài giảng của [Corey Schafer](https://www.youtube.com/user/schafer5/playlists) (anh Việt recommend)
	- [How to think like a computer scientist?](http://openbookproject.net/thinkcs/python/english3e/index.html) : sách được thể hiện dưới dạng html
	- [Google Python Class](https://developers.google.com/edu/python/)
- **Exercise, practice**
	- [Exercism](https://exercism.io/my/tracks/python) : học bằng bài tập, có nhiều ngôn ngữ khác nữa, free 100% (xem thêm [note riêng cho nó](/python-exercism-1))
	- [CheckIO](https://py.checkio.org): like exercism.
	- [Python exercises - w3resource](https://www.w3resource.com/python-exercises)
	- [PracticePython](https://www.practicepython.org/)
- **Others**:
	- [Newsletter for python](https://www.pythonweekly.com/): docs, jobs, news,....
	- [Insert Datacamp interative Python inside web/blog](https://github.com/datacamp/datacamp-light) (also for R)



## Install

- Có thể cài mọi thứ thông qua [Anaconda](https://anaconda.com), tuy nhiên trên Windows vẫn chưa tự nhận thông qua Command Prompt.
- Trên Linux hay Mac thì python tự nhận trong terminal, windows thì cần làm thêm các bước bên dưới.
- [Cài IDE Sublime Text 3](#sublime-text-3) : dùng để soạn thảo và chạy python. Thực ra cái [Spyder](#spyder) tiện hơn nhưng Spyder không chọn run theo phiên bản python được.

### Ubuntu, only use Anaconda

In the case that you have many version of python on Ubuntu and you have just installed Anaconda which also contains another version of python. **You wanna keep only one of Anaconda**

1. Follow this [question on SE](https://askubuntu.com/questions/886983/how-to-set-anaconda-as-a-default-python)
2. Add Anaconda to PATH: `export PATH=/home/thi/anaconda3/bin:$PATH`
3. Check with `which python`, if it returns `/home/thi/anaconda3/bin/python` then it works (`python -v` returns anaconda also)
4. From now, whenever you use `python`, it automatically use python inside the anaconda folder indicated as in the PATH.
5. If you wanna go back to the system default, open the `.bashrc` file and comment out settings of anaconda with `#`. That's it!


### exercism

Xem [note này]({{site.baseurl}}/python-exercism-1).


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

- See [here](http://jupyter.org/install) for full tutorial.

- **Windows**
    - [Cái này](http://jupyter.org/index.html) có sẵn nếu đã cài Anaconda.
    - Trên **Windows**, không thể chạy nó bằng dòng lệnh `jupyter notebook` như các [trang hướng dẫn](https://jupyter.readthedocs.io/en/latest/running.html) được!
    - Mà phải chạy bằng `python -m notebook` (chỉ có tác dụng sau khi đã add python path vào PATH của hệ thống như ở trên hướng dẫn)
    - Cũng có thể chạy file Jupyter Notebook có sẵn nhưng đường dẫn mặc định sau khi chạy xong (localhost:8888) không theo ý mình (ngoài /Home/), do đó, cần dùng [cmder](http://cmder.net/) (or command prompt) `cd` đến thư mục cần làm "host", sau đó chạy dòng lệnh `python -m notebook` như ở trên hướng dẫn.

- **Linux**
    - Install via Anaconda or install via **python3** as below
    - `python3 -m pip install --upgrade pip`
    - `pip install --user jupyter`
    - **Run**: `python3 -m notebook` (at where you wanna notebook run)


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
- `'{} bạn'.format{'Chào'}` returns `'Chào bạn'`
- `"Chào bạn {} và {}".format('a', 'b')` returns `'Chào bạn a và b'`
- `"Chào bạn {2} và {1}".format('a', 'b')` returns `'Chào bạn b và a'`
- Từ Python 3.6, có thể dùng `f'Chào {a}'` where `a = 'bạn'`


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

### `__name__ == __main__`

- Xem kỹ hướng dẫn ở [video này của Corey](https://www.youtube.com/watch?v=sugvnHA7ElY&t=247s).
- Nếu `print(__name__)` một file thì nó sẽ ra `__main__` nếu như mình đang thực sự chạy file đó.
- Giả sử có trường hợp mình `import` một file khác và chạy lệnh thực thi từ file được import, thì khi ấy, `__name__` là tên của file được import chứ không phải file đang chạy.
- Đó là lý do vì sao ta thường dùng `__name__ == __main__` để chắc rằng lệnh đang được chạy trên chính file này chứ không phải từ file khác dùng lệnh `import`.
- Ví dụ chỉ cần tạo 2 file có nội dung như sau rồi sau đó chạy từng file là hiểu
	- File **name_main.py**

		~~~ python
		print("__name__: {}".format(__name__))
		if __name__ == '__main__':
		    print("This one is only showed if this file runs directly!")
		~~~

	- File **name_main_import.py**

		~~~ python
		# This file is only used for import name_main.py
		import name_main
		print("__name__: {}".format(__name__))
		~~~

	- Cái này giúp cho việc phân loại các lệnh được thực thi trực tiếp hay gián tiếp bên trong 1 file.

## Operators

- `+-*/` bình thường
- `//` chia số nguyên (kết quả là interger), còn `/` thì luôn ra `real`
- Relation: `==, !=, >, <, >=, <=`
- `i = i+1` $\Leftrightarrow$ `i += 1` and others
- **Ternary conditional operator**: `b = 100 if a>10 else 0` giống như `b = (a>10)?100:0` trong C++
- `from __future__ import division` đảm bảo phép chia `/` là chia số thực, nghĩa là `1/2` ra `0.5` chứ không phải ra `0` (cf. [PEP 238](https://www.python.org/dev/peps/pep-0238/)) $\Rightarrow$ **enabled by default in Python 3.x.**
- **Đổi biến** nhanh gọn: `a, b = b, a`


## Object and Class

### Comparison

- [Tham khảo](http://abregman.com/2016/11/29/python-objects-comparison/)
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

### Condition

- `if`, `for`, `while` ([cf](https://www.programiz.com/python-programming/if-elif-else))

	``` python
	# if
	if condition:
		comands
	elif condition:
		commands
	else:
		commands
	```

- Special operator (Ternary conditional operator): `a = 100 if b>1 else 5`
- Operators trong so sánh: `==`, `!=`, `and`, `or`, `not`, `is` (object is identity, so sánh **id**)

	~~~ python
	a = [1, 2, 3]
	b = [1, 2, 3]

	a == b # True
	a is b # False
	id(a) == id(b) # True
	~~~

- **Không có switch case**, chỉ cần dùng `if elif else`
- `False` = `None`, `''`, `[]`, `{}`, '()'
- nonempty $\Rightarrow$ `True`

### Iteration

~~~ python
# loop
for num in nums:
	commands

# while
while condition:
    commands
~~~

- `break`: stop loop
- `continue`: go to next state of loop (ignore)
- `range(5)` means `[0,1,2,3,4]`
- `range(1,5)` means `[1,2,3,4]`
- Có thể dùng dạng `while True`

[Behind the scene,](https://docs.python.org/3/tutorial/classes.html#iterators) the [`for`](https://docs.python.org/3/reference/compound_stmts.html#for) statement calls [`iter()`](https://docs.python.org/3/library/functions.html#iter) on the container object. Bên trong đây có nhiều phép toán được định nghĩa, ví dụ như `__next__` (khi dùng thì chỉ cần `next()`)

<div class="mt-2 mb-2" data-datacamp-exercise data-lang="python">
<code data-type="sample-code">
s = 'abc'
it = iter(s)
print(next(it))
print(next(it))
print(next(it))

# NEW EXAMPLE
print('NEW EXAMPLE')
class Reverse:
    """Iterator for looping over a sequence backwards."""
    def __init__(self, data):
        self.data = data
        self.index = len(data)

    def __iter__(self):
        return self

    def __next__(self):
        if self.index == 0:
            raise StopIteration
        self.index = self.index - 1
        return self.data[self.index]

rev = Reverse('spam')
for char in rev:
	print(char)
</code>
</div>


## Strings, bytes, list, dictionaries, sets, tuple

### Chung, không phân biệt

- index start in python `0` (mảng, table,...)
- Chú ý `x[1:3]` là lấy thằng thứ 2 và thứ 3 chứ ko có lấy thằng thứ 4. Kiểu nó sẽ lấy $1\le i < 3$.
	Lý do là bởi đảm bảo `x[:3] + x[3:] = x`
- `"abc" + "xyz" = "abcxyz"`
- **Copy list**: dùng `a = list(b)` thay vì `a=b`
- **Methods**: `.append(<element>)` (add thêm phần tử), `.count(<element>)` (đếm phần tử `<element>` trong list), `.reverse()` (đổi order các phần tử trong list), `sort()` (sắp xếp list tăng dần)
- `sorted(<list), reverse = True)` : sắp xếp list nhưng không ảnh hưởng đến list
- Last item: `list[-1]`
- `a.extend(b)`: đưa từng phần tử của b vào a, khác với `.append()`
- `a.append('b')`: đưa phần tử `'b'` vào trong list a nhưng `a.append(c)` với `c=[1,2]` là đưa nguyên xi `[1,2]` vào a chứ không phải từng phần tử của c
- `a.remove(1)` : remove 1 from a
- `a.pop()`: remove last item from a and returns the this item.
- Liệt kê values và index

	~~~ python
	courses = ['a', 'b', 'c']
	for index, course in enumerate(courses, start = 1):
		print(index, course)

	# returns
	1 a
	2 b
	3 c
	~~~

- `course_str = ', '.join(courses)`: tạo 1 string từ courses, cách nhau bởi dấu phẩy
- Ngược lại là `.split(' - ')` chuyển từ string sang list

### Set

- [All set's methods](https://www.programiz.com/python-programming/methods/set)
- Noduplicated, unordered, mutable
- `a.intersection(b)` returns the common elements in 2 sets
- `a.difference(b)` returns different elements
- `a.union(b)` returns the union


### Empty

- list: `a=[]` hoặc `a=list()`
- tupe: `a=()` hoặc `a=tuple()`
- set: `a={}` hoặc `a=set()`


### Dictionaries

- It's mutable
- Example: `student = {'name': 'John', 'age': 25, 'course': ['Math', 'CompSci']}`
- Truy suất `student['name']`
- Xem key có trong dic không: `student.get('phone')` returns *None* nếu không tìm thấy, nếu muốn thay chữ None thì dùng `student.get('phone', 'Not Found')`.
- Thêm/update nhiều key: `student.update({'name': 'Thi', 'phone': 555})`
- Remove `del student['age']`, nếu giữa lại giá trị cái xóa thì `age = student.pop('age')`
- `len(dict)`
- See only values `student.values()`
- See key theo pairs: `student.items()`
- Truy suất only key (name, age, course): `for key in student:`
- Truy suất key và values: `for key, value in student.items():`


### Operators

- [`zip()`](https://www.programiz.com/python-programming/methods/built-in/zip): gôm từng phần tử của hai đối tượng lại với nhau.
	- Hai đối tượng này có thể cùng kiểu hoặc không (kiểu list, tupe, set).
	- Nếu số lượng hai đối tượng khác nhau thì sẽ lấy cho đến hết cái ít hơn
	- Sau đó thì có thể áp dụng phép chuyển kiểu để hiển thị ra hoặc sử dụng luôn

		<div class="row d-flex" markdown="1">
		<div class="col s12 l6" markdown="1">
		~~~ python
		strand_a = [1, 2, 3, 4, 5, 6]
		strand_b = "thi"
		kk = zip(strand_a, strand_b)
		print(tuple(kk))
		~~~
		</div>
		<div class="col s12 l6" markdown="1">
		<div class="terminal">
		((1, 't'), (2, 'h'), (3, 'i'))
		</div>
		</div>
		</div>


## Functions


- Basic

    ~~~ python
    def func():
    pass # fill later

    func() # run this function
    ~~~

- Function return không phải là value thì luôn là `None`, nó cũng cho biết function hoạt động tốt.

### With `*`

- ([Đọc SE_ref biết hết](https://stackoverflow.com/questions/36901/what-does-double-star-asterisk-and-star-asterisk-do-for-parameters)) Cái này cho phép tạo ra function với bao nhiêu argument cũng được! Với 1 `*` thì nó cho chúng ta nhập 1 list arg dạng tuple, còn với `**` thì nó cho chúng ta nhập 1 dạng pair key-val của dictionary.

    ~~~ python
    def student(*argd, **kwargs):
    commands

    courses = ['Math', 'Art']
    info = {'name': 'Thi', 'age': 28}
    std = student(*course, **info)

    # returns
    ('Math', 'Art')
    {'name': 'Thi', 'age': 28}
    ~~~

- Nói rõ hơn tí chỗ `*` này ([official_ref](https://docs.python.org/dev/tutorial/controlflow.html#more-on-defining-functions), [stackE](https://stackoverflow.com/questions/36901/what-does-double-star-asterisk-and-star-asterisk-do-for-parameters)):

- Không phải hai cái kia đại diện cho 2 biến mà mỗi cái đại diện cho 1 nhóm biến. Nếu không thêm ký hiệu `*` thì nó cứ đưa hết vô biến đầu tiên (**tuple**)

    ~~~ python
    # Understand the meaning of character * in function
    def student(*name, **note):
    print('Name: {}'.format(name))
    print('Note: {}'.format(note))

    student('Thi', 10, 11, 'Bi')
    # returns
    # Name: ('Thi', 10, 11, 'Bi')
    # Note: {}
    ~~~

- Cái `**` must be a **mapping** (e.g. dictionary)

- The `*` must be an **iterable** (what is it? see [on stack exchange](https://stackoverflow.com/questions/9884132/what-exactly-are-iterator-iterable-and-iteration)).

- Can't use more than two `*`!

- Không nhất thiết lúc nào cũng phải có đủ 1 `*` và `**`. Chúng ta có thể dùng 1 trong 2 thằng cũng được vì mỗi thằng có ý nghĩa khác nhau.

- Cả hai thằng có thể dùng với normal arg (normal arg giống như fixed arg)

- Đặc biệt

    ~~~ python
    def func(arg1, arg2, arg3, *, kwarg1, kwarg2):
        pass
    ~~~

	Such function accepts only 3 positional arguments, and everything after `*` can only be passed as keyword arguments.





## Package

- Một số package dùng trong data: `numpy` (cf [this note]({{ site.baseutl }}/python-numpy-1)), `matplotlib` (cf [this note]({{ site.baseutl }}/python-matplotlib-1)), `scikit-learn` : Machine Learning (cf [this note]({{ site.baseutl }}/python-scikit-learn-1)), `pandas` (cf [this note]({{ site.baseutl }}/python-pandas-1))

- Để cài package thường dùng `pip`: `pip3 install <package>`
- Để xài
	1. `import numpy` và xài `numpy.array()`
	2. `from numpy import array` và xài `array()` $\Rightarrow$ cách này thì người ta sẽ không biết `array()` đến từ `numpy`, code không rõ ràng cho lắm (datacamp [nói vậy](https://campus.datacamp.com/courses/intro-to-python-for-data-science/chapter-3-functions-and-packages?ex=9))
	3. `from numpy import *` là import tất cả luôn (các methods, object đều sẽ hiện hữu, cái này nó khác với cái đầu tiên, cái đầu tiên không hiện hết method, khi nào cần xài thì dùng `numpy.array` thôi (có nói trong CS50)
	4. `import matplotlib.pyplot as plt`

- Viết tắt: `import numy as np`, sau này chỉ cần `np.array()`



## Python IDE

### Spyder

- [Download](https://pythonhosted.org/spyder/installation.html) and install (có thể thông qua Annaconda)
- `clear` giống `clc` (clear hết trên khung màn hình)
- `%reset` : xóa hết biến trong workspace hiện tại (giống `clear all` trong matlab). Nếu muốn clear 1 biến cụ thể, dùng `%reset_selective <biến>`
- Chọn lệnh xong nhấn **Ctrl+Enter** để chạy code trong **Spyder**
- Chọn command, sau đó nhấn **Ctrl+I** để xem help về command đó trong **Spyder**.
- **Nhược điểm**: không chạy theo version của python được (trải nghiệm của anh Việt), dùng [Sublime Text](#sublime-text-3) có vẻ ngon hơn điểm này, giao diện của thằng kia cũng khá đẹp và thoáng.


### Sublime Text 3

<ul class="collapsible" data-collapsible="accordion">
<li>
<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
Keyboard shortcuts
</div>
<div class="collapsible-body" markdown="1">

- **Ctrl + B**: Build/Run current file
- **Ctrl + K, Ctrl + B**: Toggle sidebar
- **Ctrl + Shift + P**: Open Command Palette
- **Ctrl + R**: navigate to any function/class/symbol in the file you are currently editing
- **Ctrl + P**: quick open file
- **Ctrl + G**: đi đến bất kỳ line nào.
- **Alt + Shift + 2**: Open second window

</div>
</li>
</ul>

- Hướng dẫn từ [Corey Schafer](https://www.youtube.com/watch?v=xFciV6Ew5r4)
- Download [Sublime Text 3](https://www.sublimetext.com/3)
- Nhớ là đã cài Python rồi như ở mục đầu tiên note này.
- Cài đặt bình thường con cá hường.
- Mở lên, thử một file .py nào đó, có nội dung như sau

	~~~ python
	print("Hello World!")
	~~~

- Chạy thử: **Tools** > **Build** > chạy được bình thường.
- Install theme giống của Corey
	- **Ctrl + Shift + P** để mở **Command Palette** (**Tools** > **Command Palette...**)
	- Gõ vào và cài *Pakacge control*, giả sử đã cài xong
	- Mở CP tiếp, install tiếp hai cái sau (optional, chỉ là giao diện thôi): **Predawn** và **Material Theme**
- Sau đó mở **Preferences** > **Settings** > xóa hết cái bên **-User** và dán vào cái sau (cũng đến từ Corey)

	<ul class="collapsible" data-collapsible="accordion">
	<li>
	<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
	Xem chi tiết
	</div>
	<div class="collapsible-body" markdown="1">
	~~~
	{
		"bold_folder_labels": true,
		"caret_extra_width": 1,
		"caret_style": "phase",
		"close_windows_when_empty": false,
		"theme": "Material-Theme-Darker.sublime-theme",
		"color_scheme": "Packages/Predawn/predawn.tmTheme",
		"copy_with_empty_selection": false,
		"drag_text": false,
		"draw_minimap_border": true,
		"enable_tab_scrolling": false,
		"ensure_newline_at_eof_on_save": true,
		"file_exclude_patterns":
		[
			"*.pyc",
			"*.pyo",
			"*.exe",
			"*.dll",
			"*.obj",
			"*.o",
			"*.a",
			"*.lib",
			"*.so",
			"*.dylib",
			"*.ncb",
			"*.sdf",
			"*.suo",
			"*.pdb",
			"*.idb",
			".DS_Store",
			"*.class",
			"*.psd",
			"*.sublime-workspace"
		],
		"font_face": "Source Code Pro",
		"font_options":
		[
			"no_round"
		],
		"font_size": 15,
		"highlight_line": true,
		"highlight_modified_tabs": true,
		"ignored_packages":
		[
			"Vintage"
		],
		"line_padding_bottom": 1,
		"line_padding_top": 1,
		"match_brackets_content": false,
		"match_selection": false,
		"match_tags": false,
		"material_theme_accent_graphite": true,
		"material_theme_compact_sidebar": true,
		"open_files_in_new_window": false,
		"overlay_scroll_bars": "enabled",
		"preview_on_click": false,
		"scroll_past_end": true,
		"scroll_speed": 5.0,
		"show_definitions": false,
		"show_encoding": true,
		"show_errors_inline": false,
		"show_full_path": false,
		"sidebar_default": true,
		"theme": "Default.sublime-theme",
		"translate_tabs_to_spaces": true,
		"trim_trailing_white_space_on_save": true,
		"use_simple_full_screen": true,
		"word_wrap": true
	}
	~~~
	</div>
	</li>
	</ul>

- Cài thêm package **BracketHighlighter** (hiện bracket trên cột bên để dễ quan sát), **SidebarEnhancement** (thêm options vào trong sidebar)
- cài package **Anaconda** (cái này giống tên cái Anaconda kia thôi), sau đó cần dán đoạn settings sau vào (**Preferences** > **Package settings** > **Anaconda** > **Settings - Users**>

	<ul class="collapsible" data-collapsible="accordion">
	<li>
	<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
	Xem chi tiết
	</div>
	<div class="collapsible-body" markdown="1">
	~~~
	{
	    "auto_formatting": true,
	    "autoformat_ignore":
	    [
	        "E309",
	        "E501"
	    ],
	    "pep8_ignore":
	    [
	        "E309",
	        "E501"
	    ],
	    "anaconda_linter_underlines": false,
	    "anaconda_linter_mark_style": "none",
	    "display_signatures": false,
	    "disable_anaconda_completion": true
	}
	~~~

	Trong đây có option `auto_formatting` có chức năng tự động xóa khoảng trắng thừa nếu mình có nhập nhiều khoảng trắng quá,...
	</div>
	</li>
	</ul>

- Tạo **Build System** mới với nhiều version python khác nhau: **Tools** > **Build System** > **New Build System...** rồi dán cái sau vào (thay đường dẫn đến phiên bản python tương ứng)

	<ul class="collapsible" data-collapsible="accordion">
	<li>
	<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
	Xem chi tiết
	</div>
	<div class="collapsible-body" markdown="1">
	~~~
	{
	    "cmd": ["/usr/bin/python2.7", "-u", "$file"],
	    "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
	    "quiet": true
	}
	~~~
	</div>
	</li>
	</ul>

- Chạy code chỉ cần **Ctrl** + **B**.



### Visual Studio Code

<ul class="collapsible" data-collapsible="accordion">
<li>
<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
Xem chi tiết
</div>
<div class="collapsible-body" markdown="1">
Trong đoạn code kêu dùng Python với Spyder nhưng mà nó không tương thích với HiDPI nên quyết định chọn VSC. Không chọn Pycharm nữa vì nó nặng quá, VSC nhẹ hơn rất nhiều và làm được cho mấy cái ngôn ngữ khác được.

- Cứ mở thử một file python .py lên, nếu chưa cài extension cho VSC thì nó sẽ hỏi, nhấn vào mà cài thôi, nó sẽ cài extension mang tên Python.
- Nó cũng hỏi và đề nghị cài thêm vài cái (quên tên), cứ cài thôi.
- Nó cũng kêu chọn Python Environments gì đó, trong đó có option chọn **Anaconda** thì cứ chọn thôi (thanh dưới cùng của cửa sổ).
- Xem thêm [ở đây](https://code.visualstudio.com/docs/languages/python) để biết về VSC + Python.

[Trong course](/machine-learning-1) có dùng Ipython để mỗi lần gõ lệnh xong, quét kéo thả vào là chạy, tuy nhiên không biết torng VSC làm ở đâu. Đọc thêm [bài viết này](https://donjayamanne.github.io/pythonVSCodeDocs/docs/jupyter_getting-started/).
</div>
</li>
</ul>
