---
title: Machine Learning 1
categories: it
tags: ["machine learning"]
maths: 1
toc: 1
---

Series này note từ đầu lúc học machine learning.

{% include toc.html %}

## Chọn course & kế hoạch học tập 13.4

- [Coursera vs Udacity for Machine Learning](https://hackernoon.com/coursera-vs-udacity-for-machine-learning-f9c0d464a0eb) by Hacker Moon : so sánh hai courses học ML. Cẩn thận, cái này hơi **out of date**!
- Take this course trên **Udemy**: [https://www.udemy.com/machinelearning](https://www.udemy.com/machinelearning) (dùng Python hoặc R)
- Đọc bài này: [Machine Learning for Humans](https://medium.com/machine-learning-for-humans/why-machine-learning-matters-6164faf1df12)

## Install Python & R & Anaconda 13.4

- [Python](https://www.python.org/) đã cài sẵn trước đó lâu rùi trên máy kèm với [PyCharm bản miễn phí](https://www.jetbrains.com/pycharm/download). $\Rightarrow$ **không chọn**, chọn **Anaconda** bên dưới.
- [R](http://cran.us.r-project.org/) thì lần đầu cài, theo hướng dẫn của [bài viết này](https://medium.com/@GalarnykMichael/install-r-and-rstudio-on-windows-5f503f708027).
- [RStudio](https://www.rstudio.com/products/rstudio/download/#download)

Trên Course người ta bảo nên cài **[Anaconda](https://www.anaconda.com/download)**. Theo như giải đáp [ở đây](https://stackoverflow.com/questions/42096280/how-is-anaconda-related-to-python), thì Anaconda là một *distribution* của cả Python và R **dành riêng cho Data Science**. Nó chứa tất cả những gì cần thiết nhất cho bạn để lập trình và học machine learning, đặc biệt là Data. Nó chứa và là nơi quản lý rất nhiều thư viện (packages) cần thiết cũng như có hẳn IDE dành cho lập trình giống như PyCharm. Trong đây có

- Spyder : 1 IDE để lập trình Python. [Trang web riêng](https://pythonhosted.org/spyder/).

## Data Pre-processing

- Có những **indepedent variable** và **dependent variables**. Chúng ta dùng IV để dự đoán DV.
- Trước khi làm một model nào đều phải cần đến bước pre-processing này, rất quan trọng.
- There are 3 **libraries essentials** thường được sử dụng trong course : Xem note về [python](/python-note-1) để biết.
- 