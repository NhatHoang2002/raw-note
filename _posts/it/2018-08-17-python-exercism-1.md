---
title: Python Exercism 1
categories:
  - it
tags: ["python","exercism"]
maths: 1
toc: 1
---

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

### **[Hello World](https://exercism.io/my/solutions/c5b073e3d5b14736b3068d2e2b0cfca3)**

~~~ python
def hello():
    return "Hello, World!"

if __name__ == "__main__":
    hello()
~~~

- Lưu ý rằng, bài tập yêu cầu `return` chứ không phải `print()`!!!
- Xem thêm về [Functions](https://www.tutorialspoint.com/python3/python_functions.htm) trong python

### **[Reverse String](https://exercism.io/my/solutions/825541204dda43a9895747fec6ae09f8)**

Cách dễ và nhanh nhất, dùng **[Extended slices](https://docs.python.org/2/whatsnew/2.3.html#extended-slices)** trong python

~~~ python
def reverse(text):
    return text[::-1]
~~~

Cách "tự nhiên" hơn

~~~ python

~~~

- Xem thêm [Extended slices](https://docs.python.org/2/whatsnew/2.3.html#extended-slices)
- Xem thêm về [Strings](https://www.tutorialspoint.com/python3/python_strings.htm) trong python