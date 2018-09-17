---
title: Python 1
categories: it
tags: [python]
maths: 1
toc: 1
date: 2018-09-17
datacamp: 1
comment: 1
---

This post is used for noting the fundamental syntax of python. For more specific uses, cf [these notes](/tags#python).

{% include toc.html %}

- **Methods**: `my_dict.items()`
- **Functions**: `np.nditer(my_array)`

## Comments

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
- Print upto number of decimal

~~~ python
number = 1
print("{:.6f}".format(number)) # 1.000000
~~~

- Get the input and store to `numbers` list

~~~ python
numbers = list(map(int, input().split()))
~~~


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

---

Ví dụ chỉ cần tạo 2 file có nội dung như sau rồi sau đó chạy từng file là hiểu
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

Cái này giúp cho việc phân loại các lệnh được thực thi trực tiếp hay gián tiếp bên trong 1 file.

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

[Tham khảo](http://abregman.com/2016/11/29/python-objects-comparison/). Below is an example of comparison

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

Do đó có các comparison *rich comparison methods* or *comparison magic methods* bên trong các class/object này để "định nghĩa" luôn *thế nào là bằng, lớn, nhỏ,...* giữa các object với nhau.

~~~ python
object.__lt__(self, other) # For x < y
object.__le__(self, other) # For x <= y
object.__eq__(self, other) # For x == y
object.__ne__(self, other) # For x != y OR x <> y
object.__gt__(self, other) # For x > y
object.__ge__(self, other) # For x >= y
~~~

Xem thêm trong [cf](http://abregman.com/2016/11/29/python-objects-comparison/).


## Condition, loops

### Condition

`if`, `for`, `while` ([cf](https://www.programiz.com/python-programming/if-elif-else))

~~~ python
# if
if condition:
    comands
elif condition:
    commands
else:
    commands
~~~

Special operator (Ternary conditional operator): `a = 100 if b>1 else 5`

Operators trong so sánh: `==`, `!=`, `and`, `or`, `not`, `is` (object is identity, so sánh **id**)

~~~ python
a = [1, 2, 3]
b = [1, 2, 3]

a == b # True
a is b # False
id(a) == id(b) # True
~~~

**Không có switch case**, chỉ cần dùng `if elif else`

`False` = `None`, `''`, `[]`, `{}`, '()'

nonempty $\Rightarrow$ `True`

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

- **Looping data structures**: suppose that `world` is a dictionary, then one can use. Focus on `.items()`

	~~~ python
	for key, value in world.items():
	~~~

	We need item because <mark>dictionary is unordered</mark>

- `np.nditer()` : print continuous 2d numpy arrays used in for loop ([cf](https://docs.scipy.org/doc/numpy/reference/generated/numpy.nditer.html))
- **Pandas Series**: `brics.iterrows()`:

	~~~ python
	for label, row in brics.iterrows():
	~~~

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

---

Liệt kê values và index

~~~ python
courses = ['a', 'b', 'c']
for index, course in enumerate(courses, start = 1):
    print(index, course)

# returns
1 a
2 b
3 c
~~~

---

- `course_str = ', '.join(courses)`: tạo 1 string từ courses, cách nhau bởi dấu phẩy
- Ngược lại là `.split(' - ')` chuyển từ string sang list
- `<list>.index(<element>)`

### List

- `len(a)` gives lenght of list a (if dim of a is 1)
- `len(a)` gives number of **rows** of a (if dim a is 2)
	`len(a[0])` gives number of **columns** of a
- `map(<function>, <list>)`: apply `<function>` to each item in the `<list>`

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

- It's mutable (changeable)
- Example: `student = {'name': 'John', 'age': 25, 'course': ['Math', 'CompSci']}`
- **Don't forget ',' between elemeents**
- Truy suất `student['name']`
- Xem key có trong dic không: `student.get('phone')` returns *None* nếu không tìm thấy, nếu muốn thay chữ None thì dùng `student.get('phone', 'Not Found')`.

  - Other way: `'name' in studnet`
- Thêm/update nhiều key: `student.update({'name': 'Thi', 'phone': 555})`
- Remove `del student['age']`, nếu giữa lại giá trị cái xóa thì `age = student.pop('age')`
- `len(dict)`
- See only values `student.values()`
- See key theo pairs: `student.items()`
- See only keys : `student.keys()`
- Truy suất only key (name, age, course): `for key in student:`
- Truy suất key và values: `for key, value in student.items():`

---

define dictionary at once

~~~ python
d = {'col1':[1, 2], 'col2':[3, 4]}

# or

a = [1, 2]
b = [3, 4]
d = {'col1':a, 'col2': b}
~~~



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
// can be used 
for val_a, val_b in zip(strand_a, strand_b):
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

