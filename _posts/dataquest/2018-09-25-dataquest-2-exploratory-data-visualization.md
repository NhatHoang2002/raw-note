---
title: "DataQuest 2: Data Visualization (Exploratory & Stotytelling)"
categories: [ml, it, data]
tags: [dataquest, python, numpy, pandas, data]
maths: 1
toc: 1
comment: 1
date: 2018-10-01
---

{% assign img-url = "/images/posts/data/dataquest" %}

This note is used for my notes about the [**Data Scientist** path](https://www.dataquest.io/path/data-scientist) on **dataquest**. I take this note after I have some basics on python with [other notes](/tags#python), that's why I just write down some *new-for-me* things.

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Dataquest note 2: Pandas and Numpy fundamentals](/dataquest-2-pandas-numpy-fundamentals).
</span>
</div>

{% include more.html content="[See many other plot types](http://pandas.pydata.org/pandas-docs/stable/visualization.html)." %}

{% include toc.html %}

## Mission 142: Line Charts

{% include download.html content="[Download mission 142](/files/dataquest/mission-142.pdf)." %}

{% include more.html content="[How the Government Measures Unemployment](https://www.bls.gov/cps/cps_htgm.htm)." %}

{% include more.html content="[matplotlib ref](https://matplotlib.org)." %}

~~~ python
import pandas as pd
import matplotlib.pyplot as plt
~~~

- `pd.to_datetime(<series>)`: converts strings inside a series to a datetime objects
	- Extract `month`: `unrate['DATE'].dt.month` returns series containing `int`
- plot nothing then default axus range is `[-0.06, 0.06]`
- Plot by `plt.plot(x,y)` and the show it by `plt.show()`
- Change, rotate,... ticks: `plt.xticks(rotation=90)`
- Plot info: `plt.xlabel()`, `plt.ylabel()`, `plt.title()` (title of the plot)


## Mission 143: Multiple plots

{% include download.html content="[Download mission 143](/files/dataquest/mission-143.pdf)." %}

- Add **subplot** (<mark>top-left to bottom-right</mark>)

	~~~ python
import matplotlib.pyplot as plt
fig = plt.figure()
ax1 = fig.add_subplot(2,1,1) # nrows, ncols, plot_number
ax2 = fig.add_subplot(2,1,2)
plt.show()
	~~~

	- Use `ax1.plt(x, y)` as usual `plt.plot`
- Change size of `fig`: `plt.figure(figsize=(width_inch, height_inch))`
- Use many times `plt.plot()` to draw multi function on the same plot.
- Use `plt.plot(x, y, c="red")` to choose a color for plot. See [more here](https://matplotlib.org/api/colors_api.html).
- `plt.plot(x, y, label="<label>")` legend and then `plt.legend(loc='upper left')`, read more [here](https://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.legend).
- **Note**: there is diff between

	~~~ python
x_axis_48 = unrate.loc[0:12,["MONTH"]] # wrong
x_axis_48 = unrate[0:12]["MONTH"] # right
	~~~

## Mission 144: Bar Plots And Scatter Plots

{% include download.html content="[Download mission 144](/files/dataquest/mission-144.pdf)." %}

~~~ python
fig, ax = plt.subplots()
~~~

![Barplot positioning]({{img-url}}/matplotlib_barplot_positioning.png){:.no-border .w-700}

~~~ python
# Positions of the left sides of the 5 bars. [0.75, 1.75, 2.75, 3.75, 4.75]
from numpy import arange
bar_positions = arange(5) + 0.75

# Heights of the bars.  In our case, the average rating for the first movie in the dataset.
num_cols = ['RT_user_norm', 'Metacritic_user_nom', 'IMDB_norm', 'Fandango_Ratingvalue', 'Fandango_Stars']
bar_heights = norm_reviews[num_cols].iloc[0].values

ax.bar(bar_positions, bar_heights)
~~~

- the width of each bar is set to 0.8 by default.
- `plt.subplot()`: generate single subplot + returns both figure and axes

![Bar plot example]({{img-url}}/bar_plot_intro.png){:.no-border .w-700}

~~~ python
num_cols = ['RT_user_norm', 'Metacritic_user_nom', 'IMDB_norm', 'Fandango_Ratingvalue', 'Fandango_Stars']
bar_heights = norm_reviews[num_cols].iloc[0].values
bar_positions = arange(5) + 0.75
tick_positions = range(1,6)
width = 0.5;
fig, ax = plt.subplots()

ax.bar(bar_positions, bar_heights, width)
ax.set_xticks(tick_positions)
ax.set_xticklabels(num_cols, rotation=90)

ax.set_xlabel('Rating Source')
ax.set_ylabel('Average Rating')
ax.set_title('Average User Rating For Avengers: Age of Ultron (2015)')
plt.show()
~~~

- `ax.bar`: **verticle** bar plot.
- `ax.barh(bar_positions, bar_widths)`: create a **horizontal** bar plot
	- `bar_positions` : specify the y coordinate for the bottom sides 
	- `bar_widths`: like bar_heights
- **<mark>Note that</mark>**: there is diff between pos of `ax.barh` or `ax.bar` before or after `ax.set_xticks` or `ax.set_yticks`. It **should be before**!
- <mark>ax.set_xticklabels() takes in a list.</mark>

![Scatter plot example]({{img-url}}/scatter_plot_intro.png){:.no-border .w-700}


- `ax.scatter(x, y)`: **scatter plot** (plot with dot)

~~~ python
fig, ax = plt.subplots()
ax.scatter(norm_reviews["Fandango_Ratingvalue"], norm_reviews["RT_user_norm"])
ax.set_xlabel("Fandango")
ax.set_ylabel("Rotten Tomatoes")
plt.show()
~~~

- `ax.set_xlim(0, 5)` and `.set_ylim` to set the data limits for both axes. We **also zoom in** the plot with these commands.
- <mark>By manually setting the data limits ranges to specific ranges for all plots, we're ensuring that we can accurately compare.</mark>


## Mission 145: Histograms And Box Plots

{% include download.html content="[Download mission 145](/files/dataquest/mission-145.pdf)." %}

- Using `s.value_counts()` to display the frequency distribution.
- Don't forget to `s.sort_index()` to sort the indexes.

![Histogram example]({{img-url}}/histogram_plot_intro.png){:.no-border .w-700}

- Diff between **histogram** and **bar plots**
	+ hist describes continuous values while bar plots descibes discrete
	+ there is no space between each bin
	+ location of bars on x-axis matter in hist but not in bar plot.
	~~~ python 
# Either of these will work.
ax.hist(norm_reviews['Fandango_Ratingvalue'], 20, range=(0, 5))
ax.hist(norm_reviews['Fandango_Ratingvalue'], bins=20, range=(0, 5))
	~~~

<div class="row d-flex" markdown="1">
<div class="col s12 l7" markdown="1">
![Boxplot intro]({{img-url}}/boxplot_intro.png){:.no-border .w-500}
</div>
<div class="col s12 l5" markdown="1">
![Boxplot illustration]({{img-url}}/boxplot_understand.png){:.no-border .w-400}
</div>
</div>

- **quartile** is diff from histogram because it divides the range of values into **four** regions where each region contains 1/4th of the total values. 
	- While histograms allow us to visually estimate the percentage of ratings that fall into a **range of bins**.
	- To visualize quartiles, we need to use a **[box plot](https://www.wellbeingatschool.org.nz/information-sheet/understanding-and-interpreting-box-plots)** (box-and-whisker plot)
	- quartile is a case of **quantile** which divides the range of values into **many** equal value regions.

	~~~ python
ax.boxplot(norm_reviews["RT_user_norm"])
# multi boxplots
num_cols = ['RT_user_norm', 'Metacritic_user_nom', 'IMDB_norm', 'Fandango_Ratingvalue', 'Fandango_Stars']
ax.boxplot(norm_reviews[num_cols].values)
	~~~

## Mission 146: Guided Project: Visualizing Earnings Based On College Majors

{% include download.html content="[Ref solution](https://github.com/dataquestio/solutions/blob/master/Mission146Solutions.ipynb)." %}

- Do students in more popular majors make more money? $\Rightarrow$ Using **scatter plots**
- How many majors are predominantly male? Predominantly female? $\Rightarrow$ Using **histograms**
- Which category of majors have the most students? $\Rightarrow$ Using **bar plots**

- **Jupyter**'s magic `% matplotlib inline` so that plots are displayed inline
- Use `df.iloc[]` to return the first row formatted as a table.
- Use `df.head()` and DataFrame.tail() to become familiar with how the data is structured.
- Use `df.describe()` to generate summary statistics for all of the numeric columns.
- Number of rows : `df.shape[0]` or number of columns `df.shape[1]`
- Pandas has it own a plot method, see [here](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.plot.html).

	~~~ python
recent_grads.plot(x='Sample_size', y='Employed', kind='scatter')
# 'Sample_size' and 'Employed' are columns of recent_grads
	~~~

	We can use one-line code because of `% matplotlib inline` (of **Jupyter**)

- We can use `s.plot()`
- We can control the number of bins in series by `s.hist`

	~~~ python
recent_grads['Sample_size'].plot(kind="hist", rot=40) # rot = rotation
recent_grads['Sample_size'].hist(bins=25, range=(0,5000))
	~~~

- `scatter_matrix()` can plot scatter and hist an the same time for 2 columns ([ref](https://pandas.pydata.org/pandas-docs/stable/visualization.html#scatter-matrix-plot))

	<div class="row d-flex" markdown="1">
	<div class="col s12 l6" markdown="1">
	~~~ python
from pandas.plotting import scatter_matrix
scatter_matrix(recent_grads[['Women', 'Men']], figsize=(10,10))
	~~~
	</div>
	<div class="col s12 l6" markdown="1">
	![Boxplot intro]({{img-url}}/scatterplot_matrix_intro.png){:.no-border .w-500}
	</div>
	</div>

- Normally, when using bar plot, we need to specify the locations, labels, lenghts and widths of the bars but **pandas helps us do that**

	~~~ python
  # first 5 values in 'Women' column
  recent_grads[:5]['Women'].plot(kind='bar')

  # or better with labels
  recent_grads[:5].plot.bar(x='Major', y='Women')
	~~~

{% include more.html content="[See many other plot types](http://pandas.pydata.org/pandas-docs/stable/visualization.html)." %}



## Mission 147: Improving Plot Aesthetics

{% include download.html content="[Download mission 147](/files/dataquest/mission-147.pdf)." %}







