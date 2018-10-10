---
title: "DataQuest 4: Step 2 - Data Cleaning"
categories: [ml, it, data]
tags: [dataquest, python, numpy, pandas, data]
maths: 1
toc: 1
comment: 1
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

- 