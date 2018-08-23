---
title: Python Pandas
categories: [it,data]
tags: [python,coding,pandas,data]
maths: 1
toc: 1
date: 2018-08-20
---

This note is used only for noting pandas package in python. You can see also: [python note]({{site.baseurl}}/tags#python), [data note]({{site.baseurl}}/categories#data) or [machine learning note]({{site.baseurl}}/categories#ml).

{% include toc.html %}

## Documentation

- *[pandas](https://pandas.pydata.org/)* is an open source, BSD-licensed library providing high-performance, easy-to-use data structures and data analysis tools for the [Python](https://www.python.org/) programming language
- [Official pandas doc](http://pandas.pydata.org/pandas-docs/stable/search.html?q=head%28%29&check_keywords=yes&area=default) (use the search function)


## Installation

- Go with Anaconda package manager
- Usage: `import pandas as pd`

## Input

- `train = pd.read_csv(<file>)`
- `train.head()` ([cf](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.head.html)) : first 5 rows (default) of the data set, for a quick look in the data. You can use `.head(n=<number>)` to show `<number>` rows instead of 5.
- `train.tail()` : last 5 rows
- `train.info()` : show dtype of dataframe
- `train.describe()` ([cf](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.describe.html)) : look on distributions, dispersion, shape of dataset,... to have a general look on the dataset (more understanding on dataset)


## `iloc`

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