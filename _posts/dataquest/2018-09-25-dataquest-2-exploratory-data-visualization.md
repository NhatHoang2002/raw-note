---
title: "DataQuest 2: Exploratory Data Visualization"
categories: [ml, it, data]
tags: [dataquest, python, numpy, pandas, data]
maths: 1
toc: 1
comment: 1
date: 2018-09-28
---

{% assign img-url = "/images/posts/data/dataquest" %}

This note is used for my notes about the [**Data Scientist** path](https://www.dataquest.io/path/data-scientist) on **dataquest**. I take this note after I have some basics on python with [other notes](/tags#python), that's why I just write down some *new-for-me* things.

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Dataquest note 2: Pandas and Numpy fundamentals](/dataquest-2-pandas-numpy-fundamentals).
</span>
</div>

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
- 




