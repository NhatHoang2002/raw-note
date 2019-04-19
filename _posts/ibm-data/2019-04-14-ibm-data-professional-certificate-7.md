---
layout: post
title: "IBM Data Course 7: Data Visualization with Python"
categories: [data, python]
tags: [data, ibm data, python, matplotlib, seaborn, pandas]
toc: 1
comment: 1
---

{% assign img-url = '/images/posts/data/ibm' %}

This note was first taken when I learnt the [IBM Data Professional Certificate course](https://www.coursera.org/specializations/ibm-data-science-professional-certificate) on Coursera.

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Course 6](/ibm-data-professional-certificate-6).
</span>
</div>

{% include more.html content="[Go to Course 8](/ibm-data-professional-certificate-8)." %}

{% include toc.html %}

## Week 1: Introduction to Data Visualization Tools

<p markdown="1" class="thi-warning">
<i class="material-icons mat-icon">error</i>
The lab didn't work!!! Problem with file xls, it is not shared!
</p>

- **Tools**: matplotlib, seaborn, folium.
- **Dataset**: immigration to Canada from 1980 to 2013.
- **pandas** is a python library for data manipulation and analysis. 

### Introduction to Data Visualization

- **Why build visuals?**
	- For exploratory data analysis
	- Communicate data clearly
	- Share unbiased representation of data
	- USe them to support recommendations to different stakeholders
- **Remember**: *Less is more attractive / effective / impactive*!
	- Remove everything that can be distracting from the main message.
	- Remove border
	- Remove background
	- Don't use 3D, just 2D
	- Using different color (make the main one be diff from the others)
		![Simpler is better]({{img-url}}/ibm-6-23.jpg){:.w-700}
	-  Checkout [DarkHorseAnalytics](https://www.darkhorseanalytics.com/) for more techniques how to clean and make clear data.

### Matplotlib

- **Matplotlib Architecture** has 3 layers ([check more](http://aosabook.org/en/matplotlib.html))
	- Scripting layer (pyplot)
	- Artist layer (Artist)
	- Backend layer (FigureCanvas, Renderer, Event)
- Create 1000 random numbers using numpy: `np.random.randn(1000)`
- Check the lab for more.

### Line plots

- The **best use case for a line plot** is when you have a continuous dataset and you're interested in visualizing the data over a period of time. 

## Week 2: Basic and Specialized Visualization Tools

<p markdown="1" class="thi-warning">
<i class="material-icons mat-icon">error</i>
The lab didn't work!!! Problem with file xls, it is not shared!
</p>

- **Area plot** (area chart or area graph), based on line plot
	![Area plot]({{img-url}}/ibm-6-24.jpg){:.w-700}
	~~~ python
	import matplotlib as mpl
	import matplotlib.pyplot as plt
	df.plot(kine="area")
	plt.show()
	~~~
- **Histogram**: A histogram is a way of representing the frequency distribution of a numeric dataset. Using **bins**.
	- `df.plot(kind="hist")`
	- bin's edges are aligned to the horizontal axis
		~~~ python
		count, bin_edges = np.histogram(df['2013'])
		df['2013'].plot(kind='hist', xticks = bin_edges)
		~~~
- **Bar charts**: It is commonly used to compare the values of a variable at a given point in time.
	![Bar charts]({{img-url}}/ibm-6-25.jpg){:.w-700}
- **Pie chart**: A pie chart is a circular statistical graphic divided into slices to illustrate numerical proportion. 
	- [Pie chart or Bar chart?](https://www.surveygizmo.com/resources/blog/pie-chart-or-bar-graph/)
- **Box plot**:

## Week 3: Advanced Visualizations and Geospatial Data

<p markdown="1" class="thi-warning">
<i class="material-icons mat-icon">error</i>
A part of the lab didn't work!!! Problem with file xls, it is not shared! You can check the other part that works [here](/files/ibm/DV0101EN-3-5-1-Generating-Maps-in-Python-py-v2.0.html).
</p>

- **Waffle Charts**: A waffle chart is a great way to visualize data in relation to a whole or to highlight progress against a given threshold. **matplotlib** doesn't have a built-in function to build waffle chat.
	![Waffle charts]({{img-url}}/ibm-6-26.jpg){:.w-700}
- **Word cloud**: A word cloud is simply a depiction of the importance of different words in the body of text. **matplotlib** doesn't have a built-in function to build word cloud. There is another library.
	![Word cloud]({{img-url}}/ibm-6-27.jpg){:.w-700}
- **Seaborn and regression plots**: It was built primarily to provide a high-level interface for drawing attractive statistical graphics, such as regression plots, box plots, and so on. Seaborn makes creating plots very efficient. Therefore with Seaborn you can generate plots with code that is 5 times less than with Matplotlib.
- **Folium**: Folium is a powerful data visualization library in Python that was built primarily to help people visualize **geospatial data**.
	- **Choropleth Maps**: A choropleth map is a thematic map in which areas are shaded or patterned in proportion to the measurement of the statistical variable being displayed on the map, such as population density or per capita income. The higher the measurement the darker the color. 
		![Choropleth Maps]({{img-url}}/ibm-6-28.jpg){:.w-700}
	- [Examples](https://deparkes.co.uk/2016/06/10/folium-map-tiles/) of folium map styles.
		- **stamen toner** : great for visualizing and exploring river meanders and coastal zones. 
		- **stamen terrain** : great for visualizing hill shading and natural vegetation colors.

## Assignment

- Install **folium** after installing Anaconda ([cf](https://pypi.org/project/folium/)): `conda install -c conda-forge folium`