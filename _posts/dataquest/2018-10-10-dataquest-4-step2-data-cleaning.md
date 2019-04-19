---
layout: post
title: "DataQuest 4: Step 2 - Data Cleaning"
categories: [data,python]
tags: [dataquest, python, numpy, pandas, data]
maths: 1
toc: 1
comment: 1
date: 2018-10-17
---

{% assign img-url = "/images/posts/data/dataquest" %}

This note is used for my notes about the [**Data Scientist** path](https://www.dataquest.io/path/data-scientist) on **dataquest**.

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Dataquest 3: Step 2 - Data Visualization (Exploratory & Stotytelling)](/dataquest-2-exploratory-data-visualization).
</span>
</div>

## Mission 293 - Data cleaning basics (Step 1)

{% include download.html content="[Download mission 293](/files/dataquest/mission-293.pdf)." %}

- **The most common encodings**: UTF-8 (the default for Python), Latin-1 (also known as ISO-8895-1), Windows-1251.

  ~~~ python
  laptops = pd.read_csv("laptops.csv", encoding="Latin-1")
  laptops.info() # see the general info of the dataset
  ~~~

	`UTF-8` is default, no need to be indicated when using.

- `df_test = df.copy()`: copy data frame for testing
- `df.columns` returns an index object with the label of each columns.
- Cleans strings

  ~~~ python
  def clean_col(col):
    col = col.strip() # removes white space from the start and end
    col = col.replace("(","")
    col = col.replace(")","")
    col = col.lower()
    return col
  laptops.columns = [clean_col(c) for c in laptops.columns]
  ~~~

- `series.str.replace("text1", "text2")`: look like `string.replace()` but a vectorized version for many items.
  - **Tips**: we can use `s.str.replace().str.replace()`(<mark>many times</mark>)
- `s.astype(float)` or `s.astype(int)` change to numeric for all items in a series
- `df.rename({"<old-label>": "<new-label>"}, axis=1, inplace=True)`

  ~~~ python
  laptops["screen_size"] = laptops["screen_size"].str.replace('"','').astype(float)
  laptops.rename({"screen_size": "screen_size_inches"}, axis=1, inplace=True)
  ~~~

  ![Cleaning workflow](/images/posts/data/dataquest/cleaning_workflow.svg){:.no-border .w-700}

- **Tips:** method chaining : we ue as below so that if there is any error, we can know exactly which line.

	~~~ python
  laptops["weight"] = (laptops["weight"]
             			  .str.replace("kg","")
                        .astype(float)
	                  )
	~~~

	<mark>There is `()` before and after.</mark>

- `s.str.split()`: splits strings inside a series by whitespace (`[s t r]` becomes `[s,t,r]`)
	- `s.str.split(n=1)` : performs a single split at first whitespace
	- Note that, after splitting, there will be a **list inside this series**, not good!
- We can expand to a new df after splitting: `s.str.split(n=1, expand=True)`
- Couple: `s.str.split(n=1, expand=True).iloc[:, 0]` (select first column)
- **Split from the right**: `s.str.rsplit()`
- Example

  ~~~ python
  screen_res = laptops["screen"].str.rsplit(n=1, expand=True)
  # giving the columns string labels makes them easier to work with
  screen_res.columns = ["A", "B"]
  # for rows where the value of column "B" is null, fill in the
  # value found in column "A" for that row
  screen_res.loc[screen_res["B"].isnull(), "B"] = screen_res["A"]
  print(screen_res.iloc[:10])
  ~~~

- `s.map(<dictionary>)` to fix a list of "the same" values but diff typing. If there is no value in `s` which are in the key of `<dictionary>`, all will be mapped to `NaN`. Thus, <mark>include both correct or incorret values in dictionary</mark>

  ~~~ python
  mapping_dict = {
      'Android': 'Android',
      'Chrome OS': 'Chrome OS',
      'Linux': 'Linux',
      'Mac OS': 'macOS',
      'No OS': 'No OS',
      'Windows': 'Windows',
      'macOS': 'macOS'
  }
  laptops["os"] = laptops["os"].map(mapping_dict)
  ~~~

- Identify which values are missing: using `df.info()` or `df.isnull()`

  ~~~ python
  laptops.isnull().sum()
  ~~~

- **Dropping**: Removing rows/columns having null values. Use `df.dropna()`
- `df = df.dropna()`: removes rows, `df.dropna(axis=1)`: removes columns
- `df.drop('<column>', axis=1)` removes a column and without `aixs` to remove a row.

  - `df.drop([<list-of-columns>])`
- **Reorder column**:
	- `df.columns`: list of all columns
	- `df.to_csv()`: save out CSV file and option `index=False` if we don't want to save the index labels.

  ~~~ python
  cols = ['manufacturer', 'model_name', 'category', 'screen_size_inches',
          'screen', 'cpu', 'cpu_manufacturer',  'cpu_speed', 'ram_gb',
          'storage_1_type', 'storage_1_capacity_gb', 'storage_2_type',
          'storage_2_capacity_gb', 'gpu', 'gpu_manufacturer', 'os',
          'os_version', 'weight_kg', 'price_euros']

  laptops = laptops[cols]
  laptops.to_csv("laptops_cleaned.csv", index=False)
  ~~~

## Mission 136 - Data Cleaning <mark>Walkthrough</mark>

{% include download.html content="[Download mission 136](/files/dataquest/mission-136.pdf)." %}

{% include more.html content="[See Jupyter notebook walkthrough](https://github.com/dinhanhthi/Dataquest-Learning/blob/master/step2/data_cleaning)." %}

- In python notebook, don't use `print()` to display df, just call the name of this df, it will automatically appears.
- To combine dataframes together, we need a unique column to be a ID for all df (`DBN` in this case)
- Combine 2 df, use `pd.concat`
- Copy a column to another one.
- Use `s.apply()` to apply a function to all coponents inside a series/pf
- Convert to numeric `pd.to_numeric`

## Mission 137 - Data Cleaning <mark>Walkthrough</mark>

{% include download.html content="[Download mission 137](/files/dataquest/mission-137.pdf)." %}

{% include more.html content="[See Jupyter notebook walkthrough](https://github.com/dinhanhthi/Dataquest-Learning/blob/master/step2/data_cleaning)." %}

- Split a df into unique groups base all a column: `df.groupby(<column>)`
- Use the [`df.agg()`](http://pandas.pydata.org/pandas-docs/stable/groupby.html#aggregation) method on the resulting `df.groupby` object, along with the `np.mean()` function as an argument, to calculate the average of each group. The result will take the column as indexes
- Use [`df.reset_index()`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.reset_index.html) to reset the column out of index.
- Because we are investigating the data in the most recent time, we thus only consider the data in the recent years!
- [`pd.merge()`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.merge.html) to merge dataframes: inner, outer, left and right type of merge: depends on the importance of the data, we will use an appropriate merge method. For example, if we want to keep the data on the left, we use left merge method because if we use the right one, there are many data will be deleted.
- We can fill in missing data in pandas using the [`df.fillna()`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.fillna.html) method. **Need to assign back to the df**.
- Compute the mean of every column using [`df.mean()`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.mean.html). If we pass the results of the df.mean() method into the df.fillna() method, pandas will fill in the missing values in each column with the mean of that column. 


## Mission 138 - Data Cleaning Walkthrough: Analyzing and Visualizing the Data

{% include download.html content="[Download mission 138](/files/dataquest/mission-137.pdf)." %}

{% include more.html content="[See Jupyter notebook walkthrough](https://github.com/dinhanhthi/Dataquest-Learning/blob/master/step2/data_cleaning)." %}

- **[R value](https://en.wikipedia.org/wiki/Pearson_correlation_coefficient)**: Correlations tell us <mark>how closely related two columns are</mark>. We'll be using the r value, also called Pearson's correlation coefficient, which measures how closely two sequences of numbers are correlated. Both are increasing or decreasing or different at the same time!
- In general, <mark>r values above .25 or below -.25 are enough to qualify a correlation as interesting</mark>.
- We can use the pandas [`df.corr()`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.corr.html) method to find correlations between columns in a dataframe. The method returns a new dataframe where the index for each column and row is the name of a column in the original data set.
- Apply plots for a df: `df.plot.scatter(x="A", y="B")`
- Using **multi conditionals** for columns in df, we apply each condition separately **instead of using** `df[df["a"]=="x" and df["b"]=="y"]`
- We learned how to use the [**Basemap package**](http://matplotlib.org/basemap/) to create maps in the Visualizing Geographic Data mission. The Basemap package enables us to create high-quality maps, plot points over them, and then draw coastlines and other features.
- Convert the pandas series containing the latitude and longitude coordinates to lists using the [`s.tolist()`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.tolist.html) method.
- Basemap also supports **[scatter plot](http://matplotlib.org/basemap/api/basemap_api.html#mpl_toolkits.basemap.Basemap.scatter)**

## Mission 139 - Guided Project: Analyzing NYC High School Data

{% include more.html content="[See Jupyter notebook walkthrough](https://github.com/dinhanhthi/Dataquest-Learning/blob/master/step2/data_cleaning)." %}




