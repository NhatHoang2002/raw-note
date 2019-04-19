---
layout: post
title: "Python 0 : Docs & Settings"
categories: [it, python]
tags: [python]
maths: 1
toc: 1
date: 2018-09-25
comment: 1
snippet: 1
---

This post is only for installing and setting up python on computer. All documentation resources are also presented here.

{% include toc.html %}


## Documentation

- **For checking everytime**
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
	- [Automate the Boring Stuff with Python](https://automatetheboringstuff.com/) : free ebook for python (there is a corresponding course on Udemy)
	- [Python course for Data Science](https://courses.cognitiveclass.ai/courses/course-v1:Cognitiveclass+PY0101EN+v2/progress) on Big Data University.
	- [Python for Data Analysis](https://github.com/wesm/pydata-book), 2nd Edition by Wes McKinney, published by O'Reilly Media.
- **Exercise, practice**
    - **[HackerRank](https://www.hackerrank.com/domains/python)** : challenge you in different problems and exercises.
    - Others with the same type as HackerRank: [Exercism](https://exercism.io/my/tracks/python), [CheckIO](https://py.checkio.org), 
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
	- If using above command, it's only saved for the current workspace, after the computer restarts, it disappears.
	- Open `~/.profile` and then paste above command to it.
	- Excute: `source ~/.profile` in order to immediately reflect changes to your current terminal instance
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



## Miscellaneous

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
	In details
	</div>
	<div class="collapsible-body" markdown="1">
	~~~
{
	"cmd": ["/home/thi/anaconda3/bin/python", "-u", "$file"],
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
