---
title: Machine Learning 1
categories: it
tags: ["machine learning"]
maths: 1
toc: 1
---

Series này note từ đầu lúc học [machine learning trên Udemy](https://www.udemy.com/machinelearning).

{% include toc.html %}

## Chọn course & kế hoạch học tập 13.4

- [Coursera vs Udacity for Machine Learning](https://hackernoon.com/coursera-vs-udacity-for-machine-learning-f9c0d464a0eb) by Hacker Moon : so sánh hai courses học ML. Cẩn thận, cái này hơi **out of date**!
- Take this course trên **Udemy**: [https://www.udemy.com/machinelearning](https://www.udemy.com/machinelearning) (dùng Python hoặc R)
- Đọc bài này: [Machine Learning for Humans](https://medium.com/machine-learning-for-humans/why-machine-learning-matters-6164faf1df12)

## Install Python & R & Anaconda 13.4

Chỉ cần cài duy nhất **[Anaconda](https://www.anaconda.com/download)** là đủ. Bên trong nó có nhiều cái cho mình lựa chọn cài, nên cài 

- [Python](https://www.python.org/) đã cài sẵn trước đó lâu rùi trên máy kèm với [PyCharm bản miễn phí](https://www.jetbrains.com/pycharm/download). $\Rightarrow$ **không chọn**, chọn **Anaconda** bên dưới.
- [R](http://cran.us.r-project.org/) thì lần đầu cài, theo hướng dẫn của [bài viết này](https://medium.com/@GalarnykMichael/install-r-and-rstudio-on-windows-5f503f708027).
- [RStudio](https://www.rstudio.com/products/rstudio/download/#download)

Trên Course người ta bảo nên cài **[Anaconda](https://www.anaconda.com/download)**. Theo như giải đáp [ở đây](https://stackoverflow.com/questions/42096280/how-is-anaconda-related-to-python), thì Anaconda là một *distribution* của cả Python và R **dành riêng cho Data Science**. Nó chứa tất cả những gì cần thiết nhất cho bạn để lập trình và học machine learning, đặc biệt là Data. Nó chứa và là nơi quản lý rất nhiều thư viện (packages) cần thiết cũng như có hẳn IDE dành cho lập trình giống như PyCharm. Trong đây có

- **Spyder** : 1 IDE để lập trình Python. [Trang web riêng](https://pythonhosted.org/spyder/).

## Dataset

| Country | Age | Salary | Purchased |
|---------|-----|--------|-----------|
| France  | 44  | 72000  | No        |
| Spain   | 27  | 48000  | Yes       |
| Germany | 30  | 54000  | No        |
| Spain   | 38  | 61000  | No        |
| Germany | 40  |        | Yes       |
| France  | 35  | 58000  | Yes       |
| Spain   |     | 52000  | No        |
| France  | 48  | 79000  | Yes       |
| Germany | 50  | 83000  | No        |
| France  | 37  | 67000  | Yes       |

## Data Pre-processing & Importing Dataset

- Có những **indepedent variable** và **dependent variables**. Chúng ta dùng IV để dự đoán DV.
- Trước khi làm một model nào đều phải cần đến bước pre-processing này, rất quan trọng.
- There are 3 **libraries essentials** thường được sử dụng trong course : Xem note về [python](/python-note-1) để biết.

Python (cần phân biệt cột dependent vars và independent vars)

~~~ python
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd

# Importing the dataset

dataset = pd.read_csv('Data.csv')
x = dataset.iloc[:, :-1].values
y = dataset.iloc[:,-1].values
~~~

R (không cần phân biệt depden and indepdend vars trong dataset)

~~~ R
dataset = read.csv('Data.csv')
~~~

## OOP: classes & objects

- **class**: một mẩu chung (bản thiết kế nhà)
- **object**: vật áp dụng class (cái nhà), có thể có nhiều object với cùng class.
- **methods**: tools take some actions on the objects defined in the class.

<ul class="collapsible" data-collapsible="accordion">
<li>
<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
Đọc thêm để hiểu về OOP
</div>
<div class="collapsible-body" markdown="1">
Tham khảo [trang này](https://www.codenewbie.org/blogs/object-oriented-programming-vs-functional-programming).

- OPP: tạo class chung cho tất cả object để mỗi lần tạo một obj mới là có sẵn hết mấy cái đặc tính (bao gồm cả obj và methods)
- FP (functional programming): tách biệt rõ hai thằng này ra. Biến 1 nơi, hàm một nơi, khi cần thao tác thì đưa biến vào hàm.

Sự khác nhau

- Có thể tác động và sử dụng từng hàm riêng lẻ trong FP, tuy nhiên OPP thì mỗi lần đụng tới 1 obj là đụng tới tất cả các thuộc tính của nó.
- FP tạo ra 1 biến trung gian để lưu trạng thái sau khi chỉnh sửa trong khi OPP khi chỉnh sửa thì nó sửa luôn cái obj gốc, do đó mỗi lần muốn biết giá trị của 1 obj tại 1 thời điểm thì phải chạy từ đầu.
- OOP giúp quản lý code tốt hơn, thay đổi từng obj riêng lẽ cũng tốt hơn.
- *when he deals with data about people, FP works well, but when he tries to simulate people, OOP works well.*
</div>
</li>
</ul>

## Missing Data

Chuẩn bị data để ML works correctly và phát hiện ra bị thiếu data ở một số chỗ thì phải làm sao? $\Rightarrow$ Điền vào bằng cách tính **mean** (trung bình) của những cái khác.

- Dùng class **Imputer** của **sklearn.preprocessing**

**Python**

~~~ python
from sklearn.preprocessing import Imputer
# Imputer is a class
imputer = Imputer(missing_values = 'NaN', strategy = 'mean', axis = 0)
imputer = imputer.fit(X[:,1:3]) # set imputer as a obj relating to X
X[:,1:3] = imputer.transform(X[:,1:3]) # replace missing X 
~~~

Các `strategy`:

- `mean` = giá trị trung bình $\frac{1}{n}\sum_i x_i$
- `median` = số trung vị, tức số trong dãy có vị trí ở giữa (nếu số phần tử là lẻ). Nếu số phần tử là lẻ thì nó sẽ lấy trung bình 2 số ở giữa.
- `most_frequent` = số xuất hiện thường xuyên nhất.

**R**

~~~ R
# Taking care of missing data
dataset$Age = ifelse(is.na(dataset$Age), # conditional
                     ave(dataset$Age, FUN = function(x) mean(x, na.rm = TRUE)), # if true
                     dataset$Age)  # if false
dataset$Salary = ifelse(is.na(dataset$Salary),
                        ave(dataset$Salary, FUN = function(x) mean(x, na.rm = TRUE)),
                        dataset$Salary)  
~~~

## Categorical data

Xem những biến có những cái chung, ví dụ **Country** và **Purchased** có những cái giống nhau nên cần phân loại chúng, tuy nhiên chúng đang ở dạng "text" nên cần encode sang number.

- Dùng class **LabelEncoder** của **sklearn.preprocessing**

Tuy nhiên khi chuyển text thành number thì sẽ xảy ra tình trạng **ML sẽ nghĩ thằng này LỚN HƠN thằng kia** (chuyển thành 0, 1, 2 thì nó nghĩ France lớn hơn Germany chẳng hạn). Vậy là không được! $\Rightarrow$ dùng **Dummy Encoding**.

**Dummy Encoding** có nghĩa là tách mỗi cat ra thành 1 cột riêng, hàng nào có sự hiện diện của nó thì giá trị là 1, hàng nào ko thì 0. Như vậy ML sẽ không ưu tiên thằng nào cả.

**Python**

~~~ python
from sklearn.preprocessing import LabelEncoder, OneHotEncoder

labelencoder_X = LabelEncoder()
X[:,0] = labelencoder_X.fit_transform(X[:,0]) # country

onehotencoder = OneHotEncoder(categorical_features = [0]) # which colum will be encoded
X = onehotencoder.fit_transform(X).toarray()

labelencoder_y = LabelEncoder()
y = labelencoder_Y.fit_transform(y) # purchased
~~~

**R**: không cần phải chia thành từng cột (OneHotEncoder như trên) mà chia các thành phần của cat thành các factors riêng.

~~~ R
dataset$Country = factor(dataset$Country,
                         levels = c('France','Spain', 'Germany'), # 'c' is a vector in R
                         labels = c(1, 2, 3)) # khong quan trong no ordered related
dataset$Purchased = factor(dataset$Purchased,
                         levels = c('No','Yes'), # 'c' is a vector in R
                         labels = c(0, 1)) # khong quan trong no ordered related
~~~