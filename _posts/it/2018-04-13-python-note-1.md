---
title: Python note 1
categories:
  - it
tags: ["matlab"]
maths: 1
toc: 1
---

{% include toc.html %}

## Tài liệu

- Python documentation: [http://devdocs.io/python~3.6/](http://devdocs.io/python~3.6/)
- 

## Linh tinh

- index start in python 0 (mảng, table,...)
- Documentation for python: [devdocs](http://devdocs.io/python~3.6/)
- Chú ý `x[1:3]` là lấy thằng thứ 2 và thứ 3 chứ ko có lấy thằng thứ 4. Kiểu nó sẽ lấy $1\le i < 3$.
- Chọn command, sau đó nhấn **Ctrl+I** để xem help về command đó trong Spyder.
- Chọn lệnh xong nhấn **Ctrl+Enter** để chạy code trong **Spyder**
- - `"abc" + "xyz" = "abcxyz"`
- không dùng `;` chỉ dùng thụt đầu dòng. Nếu muốn 2 lệnh trên 1 dòng thì cách nhau bởi `;`
- comment dùng `#`, multi lines dùng `'''` ở đầu và cuối.
- `y=x`, nếu `y` change thì `x` cũng change luôn. Thay vào đó, dùng `y=list(x)` hoặc `y=x[:]`
- Có thể break lines bình thường trong python, không cần dùng thêm ký hiệu gì (nhớ thụt đầu dòng vao) HOẶC dùng dấu `\`

~~~ python
a = '1' + '2' + '3' + \
    '4' + '5'
# or
a = ('1' + '2' + '3' +
    '4' + '5')
~~~


## [Pandas](http://pandas.pydata.org/) package

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
- 

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

Trong đoạn code kêu dùng Python với Spyder nhưng mà nó không tương thích với HiDPI nên quyết định chọn VSC. Không chọn Pycharm nữa vì nó nặng quá, VSC nhẹ hơn rất nhiều và làm được cho mấy cái ngôn ngữ khác được.

- Cứ mở thử một file python .py lên, nếu chưa cài extension cho VSC thì nó sẽ hỏi, nhấn vào mà cài thôi, nó sẽ cài extension mang tên Python.
- Nó cũng hỏi và đề nghị cài thêm vài cái (quên tên), cứ cài thôi.
- Nó cũng kêu chọn Python Environments gì đó, trong đó có option chọn **Anaconda** thì cứ chọn thôi (thanh dưới cùng của cửa sổ).
- Xem thêm [ở đây](https://code.visualstudio.com/docs/languages/python) để biết về VSC + Python.
  - 

[Trong course](/machine-learning-1) có dùng Ipython để mỗi lần gõ lệnh xong, quét kéo thả vào là chạy, tuy nhiên không biết torng VSC làm ở đâu. Đọc thêm [bài viết này](https://donjayamanne.github.io/pythonVSCodeDocs/docs/jupyter_getting-started/).



