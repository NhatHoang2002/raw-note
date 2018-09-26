---
title: "DataQuest 2: Exploratory Data Visualization"
categories: [ml, it, data]
tags: [dataquest, python, numpy, pandas]
maths: 1
toc: 1
comment: 1
---

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
