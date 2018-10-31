---
title: "DataQuest 3: Step 2 - Data Visualization (Exploratory & Stotytelling)"
categories: [ml, data]
tags: [dataquest, python, numpy, pandas, data]
maths: 1
toc: 1
comment: 1
date: 2018-10-10
---

{% assign img-url = "/images/posts/data/dataquest" %}

This note is used for my notes about the [**Data Scientist** path](https://www.dataquest.io/path/data-scientist) on **dataquest**. I take this note after I have some basics on python with [other notes](/tags#python), that's why I just write down some *new-for-me* things.

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Dataquest 2: Step 2 - Pandas and Numpy fundamentals](/dataquest-2-pandas-numpy-fundamentals).
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

- Add **subplot** (<mark>top-left to bottom-right</mark>) (multi plots in the same figure)

	~~~ python
import matplotlib.pyplot as plt
fig = plt.figure()
ax1 = fig.add_subplot(2,1,1) # 2rows, 1cols, plot_number 1
ax2 = fig.add_subplot(2,1,2)
plt.show()
	~~~

	- Use `ax1.plt(x, y)` as usual `plt.plot`
- Change size of figure `fig`: `plt.figure(figsize=(width_inch, height_inch))`
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

{% include download.html content="[Ref solution of project 146](https://github.com/dataquestio/solutions/blob/master/Mission146Solutions.ipynb)." %}

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

- 2 line plot in the same figure

  ~~~ python
  fig, ax = plt.subplots()
  ax.plot(women_degrees['Year'], women_degrees['Biology'], label='Women')
  ax.plot(women_degrees['Year'], 100-women_degrees['Biology'], label='Men')

  ax.tick_params(bottom="off", top="off", left="off", right="off")
  ax.set_title('Percentage of Biology Degrees Awarded By Gender')
  ax.legend(loc="upper right")
  ~~~

- [**The data-ink**](https://infovis-wiki.net/wiki/Data-Ink_Ratio) ratio is the proportion of Ink that is used to present actual data compared to the total amount of ink (or pixels) used in the entire display. (Ratio of Data-Ink to non-Data-Ink). The goal is to design a display with the <mark>highest possible data-ink ratio</mark>.
- Modify/Remove **ticks** on axes & remove axes spine: 

  ~~~ python
  ax.tick_params(bottom="off", top="off", left="off", right="off", labelbottom='off')
  # Add your code here
  ax.spines["right"].set_visible(False)
  ax.spines["left"].set_visible(False)
  ~~~

  or shorter for spines

  ~~~ python
  for key,spine in ax.spines.items():
    spine.set_visible(False)
  ~~~

## Mission 148: Color, Layout, and Annotations

{% include download.html content="[Download mission 148](/files/dataquest/mission-148.pdf)." %}

- The [Color Blind 10](http://tableaufriction.blogspot.com/2012/11/finally-you-can-use-tableau-data-colors.html) palette contains ten colors that are colorblind friendly.
- **Matplotlib** expects each value to be scaled down and to **range between 0 and 1 **(not 0 and 255 of RGB color).

  ~~~ python
  cb_dark_blue = (0/255,107/255,164/255)
  ax.plot(women_degrees['Year'], women_degrees['Biology'], label='Women', c=cb_dark_blue)
  ~~~

- Line width: `ax.plot(linewidth=2)`
- Annotation: `ax.text(<x>, <y>, <text>)`
- Big figure `fig` and then inside there are multiple plot `ax`

  ~~~ python
  fig = plt.figure(figsize=(18, 3))
  ax = fig.add_subplot(1,6,sp+1)
  ~~~

## Mission 149: Guided Project: Visualizing The Gender Gap In College Degrees

{% include download.html content="[Ref solution of project 149](https://github.com/dataquestio/solutions/blob/master/Mission149Solutions.ipynb)." %}

- `ax.set_yticks([0,100])`: just keep 0 and 100 on the y ticks, or `xticks`
- transparency: `ax.plot(c="red", alpha=0.3)`
- Horizontal line in the figure: `ax.axhline(<startpoing>)`
- <mark>Note that</mark>, all coordinate in the plot is the coordinate of the axes (depends on the data)
- Save the plots (<mark>must be used before</mark> `plt.show()`)

  ~~~ python
  plt.plot(women_degrees['Year'], women_degrees['Biology'])
  plt.savefig('biology_degrees.png')
  plt.show()
  ~~~

## Mission 152: Conditional Plots (Titanic)

{% include download.html content="[Download mission 152](/files/dataquest/mission-152.pdf)." %}

- What you need to know for now is that the resulting line is a smoother version of the histogram, called a kernel density plot. [**Kernel density plots**](https://en.wikipedia.org/wiki/Kernel_density_estimation) are especially helpful when we're comparing distributions. 
- Plot kernel density and histogram together.
  ~~~ python
  import seaborn as sns
  import matplotlib.pyplot as plt
  sns.distplot(titanic["Fare"])
  plt.show()
  ~~~

- Plot only the kernel density plot

  ~~~ python
  sns.kdeplot(titanic["Age"])
  ~~~

- Style of `seaborn` (default is `darkgrid`),

  ![Seaborm styles](/images/posts/data/dataquest/seaborn_all_styles.png){:.no-border .w-600}

- Remove axes spines in seaborn: `sns.despine()`, default, it removes top right, if one wants to remove bottom left, use `sns.despine(left=True, bottom=True)`

  ~~~ python
  sns.set_style("white")
  sns.kdeplot(titanic["Age"], shade=True)
  sns.despine(bottom=True, left=True)
  plt.xlabel("Age")
  plt.show()
  ~~~

- **Small multiple** plots (automaticallt with `seaborn`)

  ~~~ python
  # Condition on unique values of the "Survived" column.
  g = sns.FacetGrid(titanic, col="Survived", size=6)
  # For each subset of values, generate a kernel density plot of the "Age" columns.
  g.map(sns.kdeplot, "Age", shade=True)
  ~~~

  - "facet" likes "subset"
  - `col="Survived"`, number of subplots depend on the number of unique values in this column
  - `size=6`, 6 inch height for each subplot.

- **Two** conditions (`col` for condition "Survived", `row` for condition "Pclass")

  ~~~ python
  g = sns.FacetGrid(titanic, col="Survived", row="Pclass")
  g.map(sns.kdeplot, "Age", shade=True)
  sns.despine(left=True, bottom=True)
  plt.show()
  ~~~

- **Three** conditions (use `hue`) (overlap plot with the previous ones)

  <div class="row d-flex" markdown="1">
  <div class="col s12 l6" markdown="1">
  ~~~ python
  g = sns.FacetGrid(titanic, col="Survived", row="Pclass", hue="Sex")
  g.map(sns.kdeplot, "Age", shade=True)
  g.add_legend() # add legend for seaborn sns
  sns.despine(left=True, bottom=True)
  plt.show()
  ~~~
  </div>
  <div class="col s12 l6" markdown="1">
  ![3 conditions](images/posts/data/dataquest/download.png){:.no-border .w-300}
  </div>
  </div>

## Mission 150: Visualizing Geographic Data

{% include download.html content="[Download mission 150](/files/dataquest/mission-150.pdf)." %}

- basemap [toolkit](https://matplotlib.org/basemap/): Basemap is an extension to Matplotlib that makes it easier to work with geographic data.

  ~~~ bash
  # install
  conda install basemap
  # or
  conda install -c conda-forge basemap
  ~~~

- You'll want to **import matplotlib.pyplot** into your environment when you use Basemap
- <mark>Create a new basemap</mark> instance

  ~~~ python
  import matplotlib.pyplot as plt
  from mpl_toolkits.basemap import Basemap
  m = Basemap(projection='merc',llcrnrlat=-80,urcrnrlat=80,llcrnrlon=-180,urcrnrlon=180)
  ~~~

- Convert the longitude values from spherical to Cartesian

  ~~~ python
  longitudes = airports["longitude"].tolist()
  latitudes = airports["latitude"].tolist()
  x, y = m(longitudes, latitudes)
  ~~~

- A scatter plot in basemap: `m.scatter()` with the same parameters as in `plt.scatter()`.

  ~~~ python
  m = Basemap(projection='merc', llcrnrlat=-80, urcrnrlat=80, llcrnrlon=-180, urcrnrlon=180)
  longitudes = airports["longitude"].tolist()
  latitudes = airports["latitude"].tolist()
  x, y = m(longitudes, latitudes)
  m.scatter(x, y, s=1) # size of dot is 1
  m.drawcoastlines() # show the coastlines
  plt.show()
  ~~~

- A great circle between 2 points on a map. In 2D, it's a line.

~~~ python
fig, ax = plt.subplots(figsize=(15,20))
m = Basemap(projection='merc', llcrnrlat=-80, urcrnrlat=80, llcrnrlon=-180, urcrnrlon=180)
m.drawcoastlines()

def create_great_circles(df):
    for idx, s in df.iterrows():
        if abs(s["end_lat"] - s["start_lat"] < 180) and abs(s["end_lon"] - s["start_lon"] < 180):
            m.drawgreatcircle(s["start_lon"], s["start_lat"], s["end_lon"], s["end_lat"])
            
dfw = geo_routes.loc[geo_routes["source"]=="DFM"]
create_great_circles(dfw)
plt.show()
~~~

## More tools

- Creating **3D** plots using [Plotly](https://plot.ly/python/3d-scatter-plots/)
- Creating **interactive visualizations** using [bokeh](http://bokeh.pydata.org/en/latest/docs/gallery/iris.html)
- Creating **interactive map** visualizations using [folium](http://python-visualization.github.io/folium/)

{% include more.html content="[Go to Dataquest 4: Step 2 - Data Cleaning](/dataquest-4-step2-data-cleaning)." %}