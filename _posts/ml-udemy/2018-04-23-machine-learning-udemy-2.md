---
title: ML Udemy 2 - Regression
categories: [ml]
tags: [machine learning, ml udemy]
maths: 1
toc: 1
---

Series này note từ đầu lúc học [machine learning trên Udemy](https://www.udemy.com/machinelearning).

{% include toc.html %}

Regression để **dự đoán** một giá trị thực nào đó. Nếu dữ liệu các biến indepent là thời gian thì dữ liệu sẽ dự đoán tương lai, nếu các biến khác th2i sẽ dự đoán những giá trị chưa biết.

Trong phần này sẽ học

1. Simple Linear Regression
2. Multiple Linear Regression
3. Polynomial Regression
4. Support Vector for Regression (SVR)
5. Decision Tree Classification
6. Random Forest Classification

## Các bước regression

0. data preprocessing
1. fit train set
2. predict test set
- 

## Simple linear regression

Làm sao mà nó có thể fit thành các đường linear cho mình được? Có nhiều thuật toán

- Least square idea

  ![](/images/posts/ML/least-square-idea.png)

X có size là (30,1) vì nó là **matrix of feature** (independent vars), còn Y là (30,) vì nó là **vector**.

**Python**

~~~ python
# Importing the libraries
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd

# Importing the dataset
dataset = pd.read_csv('Salary_Data.csv')
X = dataset.iloc[:, :-1].values
y = dataset.iloc[:, 1].values

# Splitting the dataset into the Training set and Test set
from sklearn.cross_validation import train_test_split
X_train, X_test, y_train, y_test \
  = train_test_split(X, y, test_size = 1/3, random_state = 0)

# Feature Scaling
"""from sklearn.preprocessing import StandardScaler
sc_X = StandardScaler()
X_train = sc_X.fit_transform(X_train)
X_test = sc_X.transform(X_test)
sc_y = StandardScaler()
y_train = sc_y.fit_transform(y_train)"""

# Fitting Simple Linear Regression to the Training set
from sklearn.linear_model import LinearRegression
regressor = LinearRegression()
regressor.fit(X_train,y_train)

# Predicting the Test set results
y_pred = regressor.predict(X_test)

# Visualising the Training set results
plt.scatter(X_train, y_train, color = 'red') # plot dot real data
plt.plot(X_train, regressor.predict(X_train), color = 'blue') 
# plot line predicted on training data
plt.title('Salary vs Experience (Training set)')
plt.xlabel('Years of Experience')
plt.ylabel('Salary')
plt.show()

# Visualising the Test set results
plt.scatter(X_test, y_test, color = 'red') # plot dot real data
plt.plot(X_train, regressor.predict(X_train), color = 'blue') 
plt.title('Salary vs Experience (Test set)')
plt.xlabel('Years of Experience')
plt.ylabel('Salary')
plt.show()
~~~

**R**





