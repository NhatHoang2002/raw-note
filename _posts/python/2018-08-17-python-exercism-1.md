---
title: Python Exercism 1
categories: it
tags: [python,exercism,coding]
maths: 1
toc: 1
date: 2018-08-23
comment: 1
---

{% include toc.html %}

- Trang web chính [nằm ở đây](https://exercism.io/tracks/python/tests).
- [Main python note](/python-note-1)
- [All solutions on github](https://github.com/dinhanhthi/exercism_python)

## Install

- Cái này dành để học trên trang web [exercism.io](https://exercism.io/tracks/python/tests)
- Cài **pytest**: `pip3 install pytest pytest-cache`

### Install **CLI**

- You can follow this [walkthrough](https://exercism.io/cli-walkthrough) on exercism
- **Windows**

    <ul class="collapsible" data-collapsible="accordion">
    <li>
    <div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
    More details
    </div>
    <div class="collapsible-body" markdown="1">
    - Download [latest cli](https://github.com/exercism/cli/releases)
    - Run `start "" "%LOCALAPPDATA%\Microsoft\WindowsApps"` in cmd
    - Move all extracted files/folder from step 1 to folder *WindowsApps*
    - Verify xem thành công không bằng cách gõ vào cmd `exercism`
    - Install thành công
    - Configure CLI: `exercism configure --token=<your-token>`
    - Token is obtained from [Settings](https://exercism.io/my/settings)
    - Workspace: `C:\Users\<your-windows-username>\Exercism`
    </div>
    </li>
    </ul>

- **Ubuntu**

    <ul class="collapsible" data-collapsible="accordion">
    <li>
    <div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
    More details
    </div>
    <div class="collapsible-body" markdown="1">
    - Download [here](https://github.com/exercism/cli/releases) (choose the right package)
    - Extract: `tar -xf exercism-linux-64bit.tgz`
    - Put extracted folder to `~/bin`
        <div  class="terminal" markdown="1">
        `$ mkdir -p ~/bin`

        `$ mv exercism ~/bin`

        `$ ~/bin/exercism`

        A command-line interface for the v2 redesign of Exercism.

        Download exercises and submit your solutions.

        ...
        </div>
    - Check if `~/bin` is already in `$PATH`?

        <div class="terminal" markdown="1">
        `[[ ":$PATH:" == *":$HOME/bin:"* ]] && echo "~/bin is in PATH" || echo "~/bin is not in PATH"`
        </div>
    If it returns `~/bin is in PATH`, OK, else,

        <div class="terminal" markdown="1">
        `echo "export PATH=~/bin:$PATH" >> ~/.bash_profile`
        `source ~/.bash_profile`
        </div>

    - Check everything works? `cd` then `exercism`
    - Configure CLI: `exercism configure --token=<your-token>`
    - Token is obtained from [Settings](https://exercism.io/my/settings)
    - Workspace: `/home/<your-linux-username>/exercism`
    </div>
    </li>
    </ul>





## Workflow

- Theo mặc định, workspace sau khi cài thành công là **C:\Users\dinha\Exercism**, có thể xem workspace hiện tại bằng `exercism workspace`
- Download bài tập, ví dụ `exercism download --exercise=hello-world --track=python`
- Solve locally
	- Sau khi hoàn thành, chạy file test: `pytest hello_world_test.py`
	- Lưu ý, file bài tập là **hello_world.py** nhưng file để test là **hello_world_test.py**, [đọc thêm](https://exercism.io/tracks/python/tests).
	- Xem thêm mục bên dưới.
- Submit bài tập, ví dụ `exercism submit /path/to/file [/path/to/file2 ...]`
	- Note that, when trying to submit an exercise, make sure the solution is in the `exercism/python/<exerciseName>` directory.
	- For example, if you're submitting **bob.py** for the Bob exercise, the submit command would be something like `exercism submit <path_to_exercism_dir>/python/bob/bob.py`.

- You can skip any exercise by `exercism skip $LANGUAGE hello-world`
- Sau khi summit xong, trong command lines sẽ xuất hiện thứ giống vầy

	~~~ bash
	You can complete the exercise and unlock the next core exercise at
	https://exercism.io/my/solutions/c5b073e3d5b14736b3068d2e2b0cfca3
	~~~
	
	Đi đến địa chỉ đó, làm các bước tiếp theo để hoàn thành. Thường bài tập Hello World khá dễ nên không cần mentor check lại.

### Test a file

- Sau khi hoàn thành, chạy file test: `pytest hello_world_test.py`
- Lưu ý, file bài tập là **hello_world.py** nhưng file để test là **hello_world_test.py**, [đọc thêm](https://exercism.io/tracks/python/tests).
- Nên dùng `pytest -x --ff bob_test.py`
	- **-x**: Stop After First Failure
	- **--ff**: Failed Tests First (`pytest-cache` remembers which tests failed, and can run those tests first)


## Solutions to exercises

### Read me first

- Link bài tập chỉ khả dụng sau khi đã đăng nhập.
- Các lời giải chỉ mang tính tham khảo, có thể có nhiều lời giải khác hay hơn.
- Nên check các file **_test** đi kèm file bài tập để biết rõ hơn yêu cầu input và output là gì. Đây là file dùng để test file mình làm, họ đưa sẵn vài test cases.
- Chi tiết gợi ý bài giải + yêu cầu: [Github repo](https://github.com/dinhanhthi/exercism_python)
- Trong note này chỉ ghi chú **vài thứ cần xem** để có thể giải bài tập đó + Các **cách giải khác**

### Hello World

- [Link bài tập](https://exercism.io/my/solutions/c5b073e3d5b14736b3068d2e2b0cfca3)
- **Yêu cầu**: Viết hàm return câu "Hello, World!"
- Lưu ý rằng, bài tập yêu cầu `return` chứ không phải `print()`!!!
- Xem thêm về [Functions](https://www.tutorialspoint.com/python3/python_functions.htm) trong python


### Reverse String 

- [Link bài tập](https://exercism.io/my/solutions/825541204dda43a9895747fec6ae09f8)
- **Yêu cầu**: Nhập vào 1 chuỗi, return chuỗi tương ứng nhưng ký tự ngược lại với chuỗi đầu. Ví dụ nhập vào `abc` cho ra `cba`
- Xem thêm [Extended slices](https://docs.python.org/2/whatsnew/2.3.html#extended-slices)
- Xem thêm về [Strings](https://www.w3schools.com/python/python_strings.asp) trong python

<ul class="collapsible" data-collapsible="accordion">
<li>
<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
Cách khác
</div>
<div class="collapsible-body" markdown="1">
Cách dễ và nhanh nhất, dùng **[Extended slices](https://docs.python.org/2/whatsnew/2.3.html#extended-slices)** trong python

~~~ python
def reverse(text):
    return text[::-1]
~~~

Cách khác (cùng ý nghĩa): `return text[slice(None,None,-1)]`

Cách "tự nhiên" hơn (nhưng dài hơn)

~~~ python
def reverse(text):
    new_text = ""
    for char in reversed(text):
        new_text = new_text + char
    return new_text
~~~
</div>
</li>
</ul>

### RNA Transcription

- [Link bài tập](https://exercism.io/my/solutions/68fa6f63d0b14fc9988e7ca416d6a63a)
- **Yêu cầu**: Nhập vào chuỗi DNA, xuất ra chuỗi RNA tương ứng biết A thành U, C thành G, G thành C, T thành A.
- Ví dụ input `ACGTGGTCTTAA` phải cho ra `UGCACCAGAAUU`
- Giả sử người dùng nhập đúng chữ cái và viết hoa (không xảy ra trường hợp `A123` hay `augt`)
- Xem thêm [Python Dictionaries](https://www.w3schools.com/python/python_dictionaries.asp): unordered, changeable and indexed
- Xem thêm [translate và maketrans](https://www.programiz.com/python-programming/methods/string/translate) method trong string

<ul class="collapsible" data-collapsible="accordion">
<li>
<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
Cách khác
</div>
<div class="collapsible-body" markdown="1">
Cách 1 (dùng dictionary)

~~~ python
def to_rna(dna_strand):
    trans =	{
      "A": "U",
      "G": "C",
      "T": "A",
      "C": "G"
    }

    rna = ""
    for type in dna_strand:
        rna = rna + trans[type]
    
    return rna
~~~

Cách 2 ngắn hơn (dùng `translate` method trong string)

~~~ python
def to_rna(dna):
    return dna.translate(str.maketrans('GCTA','CGAU'))
~~~
</div>
</li>
</ul>


### Gigasecond

- [Link bài tập](https://exercism.io/my/solutions/2c33c07f99764bd988d18cee91b95e6d)
- **Yêu cầu**: Tính thời gian một người sống được $10^9$ giây. Ví dụ người dùng nhập vào `2011,4,25` thì kết quả phải là `2043,1,1,1,46,40`. Người dùng có thể nhập bất cứ thứ gì miễn sau thỏa cấu trúc `yyyy,m,d[,h,m,s]` trong đó có thể nhập hoặc không `[,h,m,s]`.
- Xem thêm [datetime](https://www.w3schools.com/python/python_datetime.asp), [more](https://docs.python.org/3.6/library/datetime.html), [examples with docs](https://pymotw.com/3/datetime/)


### Yacht (dice game)

- [Link bài tập](https://exercism.io/my/solutions/86598459fe544d9ea2153b1e260fcd72)
- **Yêu cầu**: Đây là game tên [Yacht](https://en.wikipedia.org/wiki/Yacht_(dice_game)), dưới đây là bảng điểm

	<ul class="collapsible" data-collapsible="accordion">
	<li>
	<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
	Xem bảng điểm
	</div>
	<div class="collapsible-body" markdown="1">
	~~~
	Category    		Score                   Example
	Ones            	1 × number of ones      1 1 1 4 5 scores 3
	Twos            	2 × number of twos      2 2 3 4 5 scores 4
	Threes          	3 × number of threes    3 3 3 3 3 scores 15
	Fours           	4 × number of fours     1 2 3 3 5 scores 0
	Fives           	5 × number of fives     5 1 5 2 5 scores 15
	Sixes           	6 × number of sixes     2 3 4 5 6 scores 6
	Full House      	Three of one number
					 	and two of another	    3 3 3 5 5 scores 19
	Four of a Kind  	Total of the four dice  4 4 4 4 6 scores 16
	Little Straight 	30 points               1 2 3 4 5 scores 30
	Big Straight    	30 points               2 3 4 5 6 scores 30
	Choice          	Sum of the dice         2 3 3 4 6 scores 18
	Yacht           	All dices showing the
					  same face (50 pts)      4 4 4 4 4 scores 50
	~~~
	</div>
	</li>
	</ul>

	If the dice do not satisfy the requirements of a category, the score is zero. If, for example, Four Of A Kind is entered in the Yacht category, zero points are scored. A Yacht scores zero if entered in the Full House category.

	**Task**: Given a list of values for five dice and a category, your solution should return the score of the dice for that category. If the dice do not satisfy the requirements of the category your solution should return 0. You can assume that five values will always be presented, and the value of each will be between one and six inclusively. You should not assume that the dice are ordered.
- Ví dụ input là `[1, 1, 1, 3, 5], yacht.ONES`
- Xem thêm [Anonymous/Lambda function](https://www.programiz.com/python-programming/anonymous-function) trong python
- Xem thêm về [list](https://www.tutorialspoint.com/python/python_lists.htm): duplicated, unordered,indexed, mutable
- Xem thêm về [set](https://www.programiz.com/python-programming/set): unique, unordered, immutable, unindexed
- Xem thêm về [sorted](https://www.programiz.com/python-programming/methods/built-in/sorted), lưu ý có sự khác nhau ([cf](https://stackoverflow.com/questions/22442378/what-is-the-difference-between-sortedlist-vs-list-sort))

	~~~ python
	dice = [3,2,1]
	dice.sort() == [1,2,3] # return False
	sorted(dice) == [1,2,3] # return True
	~~~

	Lý do là bởi `dice.sort()` returns `None`. Trong python, hàm trả về `None` báo hiệu nó đã xử lý xong, tại chỗ. Ở trên ta so sánh `None` với `[1,2,3]` nên nó ra `False`.


### Space Age

- [Link bài tập](https://exercism.io/my/solutions/91dd469652e74e6abf5bb7c38a1eb26f)
- **Yêu cầu**: Viết 1 class cho biết số tuổi (theo hành tinh) khi người dùng nhập vào số giây. Ví dụ nhập vào `1 000 000 000` seconds thì cho ra `31.69` Earth-years old.
- Xem thêm vè [class](https://www.programiz.com/python-programming/class).
- Xem thêm về [ký hiệu underscore](https://hackernoon.com/understanding-the-underscore-of-python-309d1a029edc) trong python


### Rational Numbers

- [Link bài tập](https://exercism.io/my/solutions/420a0c8766324adf93afd6a22cb99349)
- **Yêu cầu**: Tạo các phép toán với số hữu tỷ
- We can use some methods to define other ones
- Xem thêm [__future__](https://docs.python.org/3.6/library/__future__.html)
- Xem [object comparison](http://abregman.com/2016/11/29/python-objects-comparison/)
- Xem [.format()](https://pyformat.info/)

	~~~ python
	'{}/{}'.format(1,2) # gives "1/2"
	'{1} {0}'.format('one', 'two') # gives "two one"
	~~~

- Xem [`__str__` vs `__repr__`](https://www.pythonforbeginners.com/basics/__str__-vs-__repr)

	~~~ python
	class Point:
	...   def __init__(self, x, y):
	...     self.x, self.y = x, y
	...   def __repr__(self):
	...     return 'Point(x=%s, y=%s)' % (self.x, self.y)
	>>> p = Point(1, 2)
	>>> p
	Point(x=1, y=2)
	~~~

- Xem [math module](https://docs.python.org/3/library/math.html)
- Các phương thức `__add__`, `__sub__`, `__mul__`, .... đại diện cho các phép toán `+ - *` thông thường



### [Not-finished] Sgf Parsing

- [Link bài tập](https://exercism.io/my/solutions/98cabbde19724be7873d483c370d9fd1)
- Bài này nói về việc ghi lại các nước đi của môn cờ vây, tuy nhiên không chuyên sâu.
- Yêu cầu chỉ là khi họ nhập vào một SGF string, ví dụ, `'(;A[B](;B[C])(;C[D]))'` thì ta phải xuất ra một tree structure tương ứng (được định nghĩa trong class `SgfTree`)
- Bài này độ khó **Medium**, để sau

### [Not-finished] Bank Account

- [Link bài tập](https://exercism.io/my/solutions/04e9d69f2a154a3181ed93aacc96cd9a)
- **Medium**, làm sau.

### Pangram

- [Link bài tập](https://exercism.io/my/solutions/9aabe2664b644fc5963584d21ddce9d4)
- Pangram là câu chứa tất cả các chữ cái trong tiếng Anh (24 chữ cái), mỗi chữ xuất hiện ít nhất 1 lần. Ví dụ "*The quick brown fox jumps over the lazy dog.*" 
- **Yêu cầu**: check xem một câu nhập vào có phải là một pangram hay không.

### Hamming

- [Link bài tập](https://exercism.io/my/solutions/01050f07627743459e556f50ba9f7e59)
- [Hamming distance](https://vi.wikipedia.org/wiki/Kho%E1%BA%A3ng_c%C3%A1ch_Hamming): giữa hai chuỗi ký tự, số ký tự ở cùng vị trí khác nhau chính là khoảng cách giữa hai chuỗi.
- **Yêu cầu**: Trong bài này, yêu cầu tìm khoảng cách giữa 2 chuội DNA.
- Xem [Exception handling](https://www.programiz.com/python-programming/exception-handling)
- Others: read [zip()](https://www.programiz.com/python-programming/methods/built-in/zip), [sum()](https://www.programiz.com/python-programming/methods/built-in/sum)
- Cách khác ([cf](https://github.com/ThomasZumsteg/exercism-python/blob/master/hamming/hamming.py))

	~~~ python
	def distance(strand_a, strand_b):
	    """Counts the differences in two sequences of DNA"""
	    return sum(1 for a,b in zip(strand_a, strand_b) if a != b)
	~~~
    

### Robot name

- [Exercise link](https://exercism.io/my/solutions/ee52e50c520e4b7f9f2c1b4c5ca8d867)
- **Question**: 
- Read more [random](https://www.programiz.com/python-programming/modules/random)
- 