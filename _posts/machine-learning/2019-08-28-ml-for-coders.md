---
layout: post
title: Introduction to Machine Learning for Coders 1
categories: [ml]
tags: [machine learning, ml for coders]
maths: 1
toc: 1
---

{% assign img-url = '/images/posts/ML/ml-for-coders' %}

I take [this course](http://course18.fast.ai/ml.html) on [fast.ai](https://www.fast.ai/) to review what I've learned about ML and try something new. I take this course in parallel with [Deep Learning Specialization](https://www.coursera.org/specializations/deep-learning) on Coursera.

{% include toc.html %}

## Documentation

- [Course's repository](https://github.com/fastai/fastai) on Github.
- [Lecture's notes](https://medium.com/@hiromi_suenaga/machine-learning-1-lesson-1-84a1dc2b5236)

## Installation

- **Install PyTorch**: lên [trang chủ](https://pytorch.org/), chọn thiết lập tương ứng, nó sẽ ra một dòng lệnh cài đặt, ví dụ (tự thêm `--user` vào nếu như không mở cmd/cmder bằng quyền admin)

  ~~~ bash
  pip install --user torch===1.2.0 torchvision===0.4.0 -f https://download.pytorch.org/whl/torch_stable.html
  ~~~

- Install `fastai` package.

  ~~~ bash
  pip install --user fastai
  ~~~

- Create an environment `fastai` (nó sẽ download hết mấy cái cần thiết về và tạo thành một môi trường riêng mang tên này để sau này mình sử dụng. Mặc định, anaconda nó có môi trường tên `base` hay `root` rồi!). Xem thêm [ở đây](/python-settings#conda-environment) để biết chi tiết.

  ~~~ bash
  conda create -n fastai python=3.7 anaconda
  conda env update
  activate fastai # windows
  ~~~

## Introduction to Random Forest

{% include youtube.html content="CzdWqFTmn0Y" size="5" %}

- (perhaps) the <mark>most widely applicable</mark> machine learning model.
- Solution to "[Blue Book for Bulldozers](https://www.kaggle.com/c/bluebook-for-bulldozers)" Kaggle competition. (to the top 25% of the leaderboard)
- [How to use Jupyter Notebook](/python-settings#jupyter-notebook) on my note.
- [Wiki](https://forums.fast.ai/t/wiki-thread-lesson-1/6825) for this lesson.
- [Note](https://medium.com/@hiromi_suenaga/machine-learning-1-lesson-1-84a1dc2b5236) for this lesson by fast.ai
- [jupyter notebooks](https://github.com/fastai/fastai/tree/master/courses/ml1)



