---
title: Python Exercism 1
categories:
  - it
tags: ["python","exercism","tự học","lập trình"]
maths: 1
toc: 1
---

{% include toc.html %}

- Trang web chính [nằm ở đây](https://exercism.io/tracks/python/tests).
- [Main python note](/python-note-1)

## Install

- Cái này dành để học trên trang web [exercism.io](https://exercism.io/tracks/python/tests)
- Cài **pytest**: `pip3 install pytest pytest-cache`

### Install **CLI**

1. Download [latest cli](https://github.com/exercism/cli/releases)
2. Run `start "" "%LOCALAPPDATA%\Microsoft\WindowsApps"` in cmd
3. Move all extracted files/folder from step 1 to folder *WindowsApps*
4. Verify xem thành công không bằng cách gõ vào cmd `exercism`
5. Install thành công
6. Configure CLI: `exercism configure --token=c2562d83-65ea-4176-ab80-ff058b111cf9`

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
	
	- Đi đến địa chỉ đó, làm các bước tiếp theo để hoàn thành. Thường bài tập Hello World khá dễ nên không cần mentor check lại.

### Test file

- Sau khi hoàn thành, chạy file test: `pytest hello_world_test.py`
- Lưu ý, file bài tập là **hello_world.py** nhưng file để test là **hello_world_test.py**, [đọc thêm](https://exercism.io/tracks/python/tests).
- Nên dùng `pytest -x --ff bob_test.py`
	- **-x**: Stop After First Failure
	- **--ff**: Failed Tests First (`pytest-cache` remembers which tests failed, and can run those tests first)


## Solutions to exercises

- Link bài tập chỉ khả dụng sau khi đã đăng nhập.
- Các lời giải chỉ mang tính tham khảo, có thể có nhiều lời giải khác hay hơn.
- Nên check các file **_test** đi kèm file bài tập để biết rõ hơn yêu cầu input và output là gì. Đây là file dùng để test file mình làm, họ đưa sẵn vài test cases.

### Hello World

- [Link bài tập](https://exercism.io/my/solutions/c5b073e3d5b14736b3068d2e2b0cfca3)
- **Yêu cầu**: Viết hàm return câu "Hello, World!"
- Lưu ý rằng, bài tập yêu cầu `return` chứ không phải `print()`!!!
- Xem thêm về [Functions](https://www.tutorialspoint.com/python3/python_functions.htm) trong python

<ul class="collapsible" data-collapsible="accordion">
<li>
<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
Lời giải tham khảo
</div>
<div class="collapsible-body" markdown="1">
~~~ python
def hello():
    return "Hello, World!"

if __name__ == "__main__":
    hello()
~~~
</div>
</li>
</ul>

### Reverse String 

- [Link bài tập](https://exercism.io/my/solutions/825541204dda43a9895747fec6ae09f8)
- **Yêu cầu**: Nhập vào 1 chuỗi, return chuỗi tương ứng nhưng ký tự ngược lại với chuỗi đầu. Ví dụ nhập vào `abc` cho ra `cba`
- Xem thêm [Extended slices](https://docs.python.org/2/whatsnew/2.3.html#extended-slices)
- Xem thêm về [Strings](https://www.w3schools.com/python/python_strings.asp) trong python

<ul class="collapsible" data-collapsible="accordion">
<li>
<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
Lời giải tham khảo
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

<ul class="collapsible" data-collapsible="accordion">
<li>
<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
Lời giải tham khảo
</div>
<div class="collapsible-body" markdown="1">
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
</div>
</li>
</ul>

### Gigasecond

- [Link bài tập](https://exercism.io/my/solutions/2c33c07f99764bd988d18cee91b95e6d)
- **Yêu cầu**: Tính thời gian một người sống được $10^9$ giây. Ví dụ người dùng nhập vào `2011,4,25` thì kết quả phải là `2043,1,1,1,46,40`. Người dùng có thể nhập bất cứ thứ gì miễn sau thỏa cấu trúc `yyyy,m,d[,h,m,s]` trong đó có thể nhập hoặc không `[,h,m,s]`.
- Xem thêm [datetime](https://www.w3schools.com/python/python_datetime.asp), [more](https://docs.python.org/3.6/library/datetime.html), [examples with docs](https://pymotw.com/3/datetime/)

<ul class="collapsible" data-collapsible="accordion">
<li>
<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
Lời giải tham khảo
</div>
<div class="collapsible-body" markdown="1">
~~~ python
import datetime

def add_gigasecond(birth_date):
    gigasecond = datetime.timedelta(seconds=10**9)
    return birth_date + gigasecond
~~~
</div>
</li>
</ul>

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
	Full House      	Total of the dice       3 3 3 5 5 scores 19
	Four of a Kind  	Total of the four dice  4 4 4 4 6 scores 16
	Little Straight 	30 points               1 2 3 4 5 scores 30
	Big Straight    	30 points               2 3 4 5 6 scores 30
	Choice          	Sum of the dice         2 3 3 4 6 scores 18
	Yacht           	50 points               4 4 4 4 4 scores 50
	~~~
	</div>
	</li>
	</ul>

	If the dice do not satisfy the requirements of a category, the score is zero. If, for example, Four Of A Kind is entered in the Yacht category, zero points are scored. A Yacht scores zero if entered in the Full House category.

	**Task**: Given a list of values for five dice and a category, your solution should return the score of the dice for that category. If the dice do not satisfy the requirements of the category your solution should return 0. You can assume that five values will always be presented, and the value of each will be between one and six inclusively. You should not assume that the dice are ordered.
- Ví dụ input là `[1, 1, 1, 3, 5], yacht.ONES`

<ul class="collapsible" data-collapsible="accordion">
<li>
<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
Lời giải tham khảo
</div>
<div class="collapsible-body" markdown="1">
~~~ python

~~~
</div>
</li>
</ul>

	

	