---
title: Python matplotlib
categories: [it, data]
tags: [python, matplotlib, data]
maths: 1
toc: 1
date: 2018-09-05
---

{% assign fig = "/images/posts/python/matplotlib" %}

## Install & Doc

- `pip install matplotlib`
- [Documentation](https://matplotlib.org/) (use search function)
- `import matplotlib.pyplot as plt`


## Use?

- Grades follows distribution: `plt.hist()` (histogram)


## Basic plots

<div class="row d-flex" markdown="1">
<div class="col s12 l6" markdown="1">
~~~ python
import matplotlib.pyplot as plt
plt.plot(year,pop)
plt.show()
~~~
</div>
<div class="col s12 l6" markdown="1">

![]({{ fig }}/f1.svg){:.w-300 .no-border}

</div>
</div>

- Plot: `plt.plot()`
- Show plot: `plt.show()`
- Plot điểm (no line): `plt.scatter()`
- Change scale: `plt.xscale('log')` ([cf](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.xscale.html?highlight=xscale#matplotlib.pyplot.xscale))
- **Clear up** plot: `plt.clf`
- `plt.grid(True)` : show grid
- `plt.text(x, y , 'Text')`: display `'Text'` tại tạo độ `(x,y)`
- **Only 1 arg**: `plt.plot(y)` consider the index as `x` input


### Scatter

- Plot điểm rời rạc
- `plt.scatter(x, y, s = np.array(pop), c = col)`
- `c = list-of-color` : đổi color
- `s = np.array(pop)` : chuyển sang array
- `alpha = 0.8`: apacity of the bubble

### Histogram

- Use: `plt.hist(values, bins = 3)` and then `plt.show()`
- `bins`: chia thành mấy cụm cho dữ liệu đầu vào là `values` để thể hiện coi cụm nào có nhiều thằng nhất.


## Customization

- **Labels**: `plt.xlabel('Year')`, `plt.ylabel()`
- **Title**: `plt.title()`
- **Ticks**: `plt.yticks([0,2,3],['0','2B','4B')` Có sự tương ứng giữa 2 cái `[]`, cái sau hiển thị thay chỗ tọa độ ghi trong cái trước.
