---
title: Machine Learning 1
categories: it
tags: ["machine learning"]
maths: 1
toc: 1
date: 2018-04-19
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

## Dataset & Các bước

<ul class="collapsible" data-collapsible="accordion">
<li>
<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
Bảng dataset
</div>
<div class="collapsible-body" markdown="1">

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

</div>
</li>
</ul>

Các bước sẽ học với mỗi ML model

1. **Data Pre-processing & Importing Dataset**: import các libraries, packages cần thiết + import dataset có sẵn để chuẩn bị processing nó.
2. **Missing Data**: sẽ có trường hợp nhiều fields trong data bị missing, chúng ta cần trám hết mấy chỗ missing này lại bằng quá trình missing data này. Cách trám có nhiều cách, ví dụ lấy giá trị trung bình của mấy cái có sẵn.
3. **Categorical data**: tới bước phân loại data, nghĩa là chia các cột có những thành phần giống nhau thành 1 nhóm riêng để xử lý và label cho chúng. Trong Python thì nên dùng **Dummy Endcoding** để chia thành dạng 0,1 thay vì chia thành 1,2,3 sẽ dễ làm cho ML hiểu lầm có sự ưu tiên. Trong R thì không cần làm thế vì chúng xét thành các factors riêng biệt.
4. **Splitting dataset into training set and test set**: Bây giờ là split dataset thành training và test, training là để dạy cho ML học cách phân loại, test là để kiểm tra lại xem chúng có học tốt chưa để đối chiếu.
5. **Feature scaling**: giúp cho scale dữ liệu giữa các cột cân bằng.

## Data Pre-processing & Importing Dataset

- Có những **indepedent variable** và **dependent variables**. Chúng ta dùng IV để dự đoán DV.
- Trước khi làm một model nào đều phải cần đến bước pre-processing này, rất quan trọng.
- There are 3 **libraries essentials** thường được sử dụng trong course : Xem note về [python](/python-note-1) để biết.

Python (cần phân biệt cột dependent vars và independent vars)

~~~ python
# Importing the libraries
# -----------------------------
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd

# Importing the dataset
# -----------------------------
dataset = pd.read_csv('Data.csv')
x = dataset.iloc[:, :-1].values
y = dataset.iloc[:,-1].values
~~~

R (không cần phân biệt depden and indepdend vars trong dataset)

~~~ R
# Importing the dataset
# -----------------------------------------------
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
# Taking care of missing data
# -----------------------------
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
# -----------------------------------------------
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
# Encoding categorical data
# -----------------------------
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
# Encoding categorical data
# -----------------------------------------------
dataset$Country = factor(dataset$Country,
                         levels = c('France','Spain', 'Germany'), # 'c' is a vector in R
                         labels = c(1, 2, 3)) # khong quan trong no ordered related
dataset$Purchased = factor(dataset$Purchased,
                         levels = c('No','Yes'), # 'c' is a vector in R
                         labels = c(0, 1)) # khong quan trong no ordered related
~~~

## Splitting dataset into training set and test set

- **training set**: set để train machine learning model (những gì được học)
- **test set**: để test performance của ML model (những gì được kiểm tra)

**Python**

~~~ python
# Splitting the dataset into the training set and test set
# ----------------------------------------------------------
from sklearn.cross_validation import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state = 0)
# X: part of matrix of feature, y: part of dependent variable that associated to X
# test_size=0.2: 20% of data go to test set, 80% go to train set
# random_state: mốc để set mấy thành phần random, một số int
~~~

**R**

~~~ R
# Splitting dataset into training and test sets
# -----------------------------------------------
# install.packages('caTools') # install library in R, just do it 1 time
library(caTools) # select library
set.seed(123) # choose a seed to make random choice for data
split = sample.split(dataset$Purchased, SplitRatio = .8) 
# in python we choose .2 for test set but in R, we choose .8 for training set
# TRUE => observations go to training set, FALSE => observations go to test set
training_set = subset(dataset, split == TRUE)
test_set = subset(dataset, split == FALSE)
~~~

## Feature scaling

Ví dụ tuổi trong khoảng 35 đến 50 nhưng salary tính theo chục ngàn nên khi chia tọa độ, 1 cái là x, 1 cái là y thì scale của 2 trục nó sẽ rất khác. Vì ML sử dụng khoảng cách giữa 2 observation nhiều (cần đến khoảng cách Eucliendian)

- **Standardisation**:
  $$
  x_{std} = \dfrac{x-mean(x)}{\text{standard deviation (x)}}
  $$
- **Normalisation**: 
  $$
  x_{norm = \dfrac{x-\min(x)}{\max(x)-\min(x)}
  $$

<ul class="collapsible" data-collapsible="accordion">
<li>
<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
Standard deviation (độ lệch chuẩn)
</div>
<div class="collapsible-body" markdown="1">

A low standard deviation indicates that the data points tend to be close to the mean (also called the expected value) of the set, while a high standard deviation indicates that the data points are spread out over a wider range of values.

![Độ lệch chuẩn của normal distribution](/images/posts/sd.png){:.w-600 .no-border}

Let $X$ be a random variable with mean value $\mu$:

$$\operatorname {E} [X]=\mu$$

Here the operator E denotes the average or expected value of $X$. Then the **standard deviation** of $X$ is the quantity

$$
{\displaystyle {\begin{aligned}\sigma &={\sqrt {\operatorname {E} [(X-\mu )^{2}]}}\\&={\sqrt {\operatorname {E} [X^{2}]+\operatorname {E} [-2\mu X]+\operatorname {E} [\mu ^{2}]}}\\&={\sqrt {\operatorname {E} [X^{2}]-2\mu \operatorname {E} [X]+\mu ^{2}}}\\&={\sqrt {\operatorname {E} [X^{2}]-2\mu ^{2}+\mu ^{2}}}\\&={\sqrt {\operatorname {E} [X^{2}]-\mu ^{2}}}\\&={\sqrt {\operatorname {E} [X^{2}]-(\operatorname {E} [X])^{2}}}\end{aligned}}}
$$

**Discrete random variable**

In the case where $X$ takes random values from a finite data set $x\_1, x\_2, ..., x\_N$ with each value having the same probability, the standard deviation is

$$
\sigma ={\sqrt {{\frac {1}{N}}\left[(x_{1}-\mu )^{2}+(x_{2}-\mu )^{2}+\cdots +(x_{N}-\mu )^{2}\right]}},{\rm {\ \ where\ \ }}\mu ={\frac {1}{N}}(x_{1}+\cdots +x_{N}),
$$

or, using summation notation,

$$
\sigma ={\sqrt {{\frac {1}{N}}\sum _{i=1}^{N}(x_{i}-\mu )^{2}}},{\rm {\ \ where\ \ }}\mu ={\frac {1}{N}}\sum _{i=1}^{N}x_{i}.
$$

If, instead of having equal probabilities, the values have different probabilities, let $x\_1$ have probability $p\_1, x\_2$ have probability $p\_2,\ldots, x\_N$ have probability pN. In this case, the standard deviation will be

$$
\sigma ={\sqrt {\sum _{i=1}^{N}p_{i}(x_{i}-\mu )^{2}}},{\rm {\ \ where\ \ }}\mu =\sum _{i=1}^{N}p_{i}x_{i}.
$$

**Continuous random variable**

The standard deviation of a continuous real-valued random variable $X$ with probability density function $\rho(x)$ is

$$
{\displaystyle \sigma ={\sqrt {\int _{\mathbf {X} }(x-\mu )^{2}\,p(x)\,{\rm {d}}x}},{\rm {\ \ where\ \ }}\mu =\int _{\mathbf {X} }x\,p(x)\,{\rm {d}}x,}
$$

and where the integrals are definite integrals taken for $x$ ranging over the set of possible values of the random variable $X$.

</div>
</li>
</ul>

