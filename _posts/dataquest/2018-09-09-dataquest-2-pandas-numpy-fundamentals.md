---
title: "DataQuest 2: Step 2 - Pandas and Numpy fundamentals"
categories: [ml, it, data]
tags: [dataquest, python, numpy, pandas, data]
maths: 1
toc: 1
comment: 1
date: 2018-09-25
---

This note is used for my notes about the [**Data Scientist** path](https://www.dataquest.io/path/data-scientist) on **dataquest**. I take this note after I have some basics on python with [other notes](/tags#python), that's why I just write down some *new-for-me* things.

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Dataquest note 1](/dataquest-1).
</span>
</div>

{% include toc.html %}

## Mission 289 - Introduction to NumPy

{% include more.html content="[See Numpy notes](/tags#numpy)." %}

{% include download.html content="[Download mission 289: Introduction to numpy](/files/dataquest/mission-289.pdf)." %}


- `import numpy as np` : starts to use numpy
- `<np.ndarray> = np.array(<list-of-lists>)`
- `<np.ndarray>.shape` gives dimension shape of an array in a `tuple` type (like `list` but not be modified or immutable), e.g. `(2,3)`
- numpy display a `...` to summerize an array with a large data
- `ndarray[row, column]` or `nparray[row]`
- **Selecting**

	|                      | list of lists                     | ndarray            | note     |
	|----------------------|-----------------------------------|--------------------|----------|
	| **an element**       | `list[1][3]`                      | `ndarray[1, 3]`    |          |
	| **rows**             | `list[:3]`                        | `ndarray[:3]`      | the same |
	| **columns**          | `[row[4] for row in list]`        | `ndarray[:,4]`     |          |
	| **multiple columns** | `[[row[1], row[3]] for row in a]` | `ndarray[:,[1,3]]` |          |

- `%timeit -r 1 -n 1 python_subset()` : see the time for a single run
- **numpy** quicker than **list of list** 30 times
- **Vectorized operators** (elementwise): `+, -, *, /`, `%` (remainder when a divided by b), `**`, `//` (floor division, rounding down to the nearest number)
- Alternative for `/` is `np.divide(<ndarray1>, <ndarray2>)`
- **Max/Min/Mean/Median/Sum**: 
    - Whole array: `<ndarray.min()>` or `np.min(<ndarray>)`. The same for `max, mean, median, sum`.
    - Each row: `<ndarray.max(axis=1)>`
    - Each colum: `<ndarray.max(axis=0)>`
- **Functions vs Methods**: 
    - Functions act as stand alone segments of code that usually take an input
    - Methods are special functions that belong to a specific type of object
- `np.expand_dims(<ndarray>)`:
  ~~~ python
  zeros = [0 0 0] # zeros.shape is (3,)
  zeros_2d = np.expand_dims(zeros,axis=0) # zeros_2d.shape is (1,3)
  # axis=0 w.r.t row
  # axxis=1 w.r.t column
  ~~~
- `numpy.concatenate([<ndarray1>,<ndarray2>],axis=0)`: combine 2 ndarrays

  ~~~ python
  ones = [[ 1  1  1]
        [ 1  1  1]] # shape is (2,3)
  zeros = [ 0 0 0 ] # 1d
  zeros_2d = np.expand_dims(zeros,axis=0) # to (1,3)
  combined = np.concatenate([ones,zeros_2d],axis=0)
  # result
  # [[ 1 1 1]
  #  [ 1 1 1]
  #  [ 0 0 0]] 
  ~~~

- **Sort**: `np.argsort(<ndarray>)` gives the sorted index of `<ndarray>` (sorting follows elements in ndarray but gives the result in index)

  ~~~ python
  fruit = np.array(['o', 'b', 'a', 'g', 'c'])
  sorted_order = np.argsort(fruit) # gives [2, 1, 4, 3, 0]
  fruit[sorted_order] # gives np.array(['a', 'b', 'c', 'g', 'o'])
  ~~~

	NumPy only supports sorting in **ascending order**
	
	Can sort one column of an array then apply to the whole by `nd.array[sorted_order]`

## Mission 290 - Boolean Indexing with NumPy

{% include download.html content="[Download mission 290: Boolean Indexing with NumPy](/files/dataquest/mission-290.pdf)." %}

- `taxi = np.genfromtxt('nyc_taxis.csv', delimiter=',', skip_header=1)` : reads a text file into a NumPy ndarray.
- `<ndarray>.dtype`: see the internal datatype that has been used
- `taxi = taxi[1:]` removes the first row.
- `np.array([2,4,6,8]) < 5` gives a boolean array
- `ndarray[<bool array>]` give a new ndarray but only at True indexes of bool array (remove False indexes)

  ~~~ python
  ndadday # 4x3
  bool1 = [True False True True]
  bool2 = [True False True]
  ndarray[bool1] # takes the rows
  ndaary[:,bool2] # takes the columns
  ~~~

- `c[c[:,1] > 2, 1] = 99`
- `ndarray.shape` gives a tuple `(#rows, #columns)`.

  - `ndarray.shape[0]` gives number of rows


## Mission 291 - Introduction to Pandas

{% include download.html content="[Download mission 291: Boolean Indexing with NumPy](/files/dataquest/mission-291.pdf)." %}

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
See the [note of Pandas](/python-pandas-1).
</span>
</div>

- `import pandas as pd`
- `f500 = pd.read_csv("<file-name>", index_col=0)`
    - `type(f500)` gives `pandas.core.frame.DataFrame`
    - `f500.shape` gives a tuple `(500, 16)`
- **Series** is the pandas type for **one-dimensional** objects (columns, the 1st column is alway the header of pd obj)
  - <mark>1D pd object $\Rightarrow$ series</mark>
  - <mark>2D pd object $\Rightarrow$ dataframe</mark>
- Unlike NumPy, pandas does not use the same type for 1D and 2D arrays.
- `f500.dtypes` gives type of each column
- `f500.head()` returns first 5 rows

    - `f500.head(10) returns first 10 rows`
- `f500.tail()`
- Unlike NumPy, pandas **does not use the same type** for 1D and 2D arrays.
- Select **single element**: `df.loc["Sinopec Group", "revenues"]`
- Select **rows**:
  - Single: `df.loc["a"]`
  - List: `df.loc[["a","b"]]`
  - Slice: `df["a":"c"]` or `df.loc["a":"c"]`
- Select **columns**:
  - Single: `df["a"]` or `df.loc[:,"a"]`
	- <update /> `df["a"]` gives a df but `df.loc[:,"a"]` gives a series
  - List: `df[["a", "b"]]` or `df.loc[:,["a","b"]]`
  - Slice: `df.loc[:, ["a":"c"]]`
- Select rows in **series object**
  - Single: `s["a"]` or `s.loc["a"]`
  - List: `s[["a","b"]]` or `s.loc[["a","b"]]`
  - Slice: `s["a":"c"]` or `s.loc["a":"c"]`
- `s.describe()`: gives count, mean, std, min, 25%, 50%, 75%, max or other types. (**method chaining**)

	~~~ python
revs = f500["revenues"]
print(revs.describe())
	~~~
- There is also `dataframe.describe()`
- for **all**: `all_desc = f500.describe(include='all')`
- for only **numeric**: `print(f500.describe(include=['O']))`
- **Methods**: `.max()`, `.min()`, `.mean()`, `.median()`, `.mode()`, `.sum()` applied to both **series** and **dataframe**.
  - `df.<method>(axis=0)` or `df.<method>(axis="index")` calculate along the **row** axis. <mark>default</mark>
  - `df.<method>(axis=1)` or `df.<method>(axis="column")` calculate along the **column** axis.

~~~ python
medians = f500[["revenues", "profits"]].median(axis=0)
# we could also use .median(axis="index")
# or without axis=0 because it's default
~~~

- `s.value_counts()`: displays each unique non-null value from a series, with a count of the number of times that value is used.
	- `s.value_counts(dropna=True)` exclude null values when making calculations.
	- `s.value_counts(dropna=False)` includes also the null (normally, it doesn't)
	- `s.value_counts(normalize=True)` use percentages instead of counts 
- Top 5 most common values of a column

	~~~ python
top5_countries = f500["country"].value_counts().head()
	~~~
- `df.max(numeric_only = True)` **only** display the **numeric** columns
- We can **assign** values in pandas using **selecting** tools above (like in numpy)

	~~~ python
top5_rank_revenue["revenues"] = 0 # whole columns change to 0
top5_rank_revenue.loc["Sinopec Group", "revenues"] = 999 # 1 item
	~~~
- **boolean indexing**: 

	~~~ python
s_bool = df["<column>"] = 8 # gives a boolean series. 
result = df[s_bool] # apply to whole df, DON'T use .loc
result_name = df.loc[s_bool, "<column>"] # consider a column, USE .loc[]
	~~~

- Coupling

	~~~ python
f500.loc[f500["sector"] == "abc"] = "ABC"
	~~~

- `np.nan` = NaN


## Mission 292 - Exploring Data with pandas

{% include download.html content="[Download mission 292](/files/dataquest/mission-292.pdf)." %}

~~~ python
import pandas as pd
import numpy as np
~~~

- pandas uses NumPy objects behind the scenes to store the data.
- `.loc[]` vs `.iloc[]`
	- **l**oc: **l**abel based selection
	- **i**loc: **i**nteger position based selection
- Select:
	- an element: `df.iloc[2,0]`
	- row: `df.iloc[1]`
	- column: `df.iloc[:, 1]`
	- slices: `df.iloc[1:5]`, `df.iloc[[1,3], 1:5']`
	- list: `df.iloc[:,[1,2,5]]`
- Slice:
	- with `.loc[]`, the ending slide **is** included
	- with `.iloc[]`, the dening slice **is not** included
- The same for **series** but don't forget that series is 1-D
- **Import data** ([cf](https://www.dataquest.io/m/292/exploring-data-with-pandas/3/reading-csv-files-with-pandas))

~~~ python
# we want to use the 1st column as the row labels
f500 = pd.read_csv("f500.csv", index_col=0)
# remove the index name (text in the first line, first column)
f500.index.name = None
​~~~

- Sort the rows of `f500` by columns `employees` (it **returns** another df but does not change the df itself)

  ~~~ python
  sorted_emp = f500.sort_values(by=["employees"], ascending=False)
  ~~~

- `s.str.contains("<str>")` : check if str is in s or not

  - `s.str.contains("<str>", regex = False)` if we want to consider str as a string.
- `s.str.endswith("<str>")` : check if s ends with str or not
- `s.str.startswith("<str>")`
- `s.isnull()` or `s.notnull()` : check s contains NaN or null

  ~~~ python
  rev_change_null = f500[f500["revenue_change"].isnull()]
  print(rev_change_null[["company","country","sector"]])
  ~~~

- <mark>Important</mark> about selecting

	~~~ python
  previously_ranked["rank","revenues"] # error
  previously_ranked[["rank","revenues"]] # columns
  previously_ranked.loc["rank","revenues"] # rows
  previously_ranked.loc[:, ["rank","revenues"]] # columns

  previously_ranked.loc["rank"] # dataframe
  previously_ranked["rank"] # series

  previously_ranked.loc["rank"] - previously_ranked.loc["prev_rank"] # 2 different columns (dataframe)
  previously_ranked["rank"] - previously_ranked["prev_rank"] # 1 column (series)
	~~~
- Using boolean operators

  ~~~ python
  combined = (f500_sel["revenues"] > 265000) & (f500_sel["country"] == "China")
  combined = over_265 & china
  final_cols = ["company", "revenues"]
  result = f500_sel[combined, final_cols]
  ~~~

	or just one line

  ~~~ python
  result = f500_sel.loc[(f500_sel["revenues"] > 265000) & (f500_sel["country"] == "China"), final_cols]
  ~~~

- **Comparision operators**: `==`, `~(a==b)` (not equal)
- **Panda index alignment**. If a dataframe `food` and a series `colors` have the same index (but diff order), they can be couple with
	- `food["color"] = colors`
	- Discards any items that have an index that doesn't match the dataframe
- **<mark>Loops in df</mark>**: loop over a dataframe, it returns the column index labels, rather than the rows as we might expect.
- `s.unique()`returns **an array** of unique values from any series
- Find the average revenue for each unique country in `f500`

	~~~ python
  # Create an empty dictionary to store the results
  avg_rev_by_country = {}

  # Create an array of unique countries
  countries = f500["country"].unique()

  # Use a for loop to iterate over the countries
  for c in countries:
	# Use boolean comparison to select only rows that
	# correspond to a specific country
	selected_rows = f500[f500["country"] == c]
	# Calculate the mean average revenue for just those rows
	mean = selected_rows["revenues"].mean()
	# Assign the mean value to the dictionary, using the
	# country name as the key
	avg_rev_by_country[c] = mean
	~~~


## Mission 294 - Guided Project: Exploring Ebay Car Sales Data

{% include download.html content="[See the ref solution](https://github.com/dataquestio/solutions/blob/master/Mission294Solutions.ipynb)." %}

- `s.sort_index(ascending=False)` to sort index of series
- `s.sort_values()` : to sort values
- See first 10 letters of each row on each column: `autos["ad_created"].str[:10]`
- `df[(df["col"] > x ) & (df["col"] < y )]` = `df[df["col"].between(x,y)]` to take the values of column "col" between `x` and `y`.
- `s.value_counts().sort_index(ascending=True)`: sort values of `s` for easier examination.
- `autos = autos[autos["price"].between(1,351000)]`: only take values between an amount.
- **element-wise logical** comparison: `&` (and), `==` (equal), `|` (or), `~` (not)
- number of current examined elements: `autos.shape[0]`
- Find how many "less or greater" in percent:
	~~~ python
(~autos["registration_year"].between(1900, 2016)).sum() / autos.shape[0]
	~~~
- Many ways to select rows in a dataframe that fall within a value range for a column.
	~~~ python
autos = autos[autos["registration_year"].between(1900, 2016)]
	~~~
- A series will present a (hide) column `index` and a column `value`. We can use `s.index` to show the indexes of this series.
- **Combine the data from both series objects into a single dataframe**
	- [pandas series constructor](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html)
	- [pandas dataframe constructor](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html)
- **Quickly** create a

	~~~ python
  # pandas series:
  s = pd.Series([True, True, False, True])
  # or from a dictionary abc
  s = pd.Series(abc) # key in dict becomes the index in series

  # pandas dataframe: 
  df = pd.DataFrame(np.random.randn(6,4),index=dates,columns=list('ABCD'))
  # or from a series
  df = pd.DataFrame(s, columns=["<name>"]) # column name will be set to 0 by default
	~~~

- **Add many series into a df**: convert 1 series to df and then add other series to this df as new columns.


{% include more.html content="[Go to Dataquest 3: Step 2 - Data Visualization (Exploratory & Stotytelling)](/dataquest-2-exploratory-data-visualization)." %}
