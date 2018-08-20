---
title: Python Pandas
categories:
  - it
tags: ["python","tự học","lập trìnnh","pandas"]
maths: 1
toc: 1
date: 2018-08-20
---

*[pandas](https://pandas.pydata.org/)* is an open source, BSD-licensed library providing high-performance, easy-to-use data structures and data analysis tools for the [Python](https://www.python.org/) programming language

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