---
title: Python note 1
categories:
  - it
tags: ["matlab"]
maths: 1
toc: 1
---

{% include toc.html %}

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



