---
title: Data - Kaggle
categories: [ml, it, data]
tags: [machine learning, data codecademy, kaggle]
maths: 1
toc: 1
date: 2018-09-03
---

This note is used only for noting everything relating to Kaggle.

{% include toc.html %}

## Installing Kaggle

0. See [this tutorial](https://github.com/Kaggle/kaggle-api)
1. Use `pip install --user kaggle` (do not use `sudo`!)
2. Then kaggle is installed in `~/.local/bin`
3. Access `kaggle.com/<your-account>/account` and then click **Create new API Token** and then download a kaggle.json file 
4. Place this file to `~/.kaggle` (Linux/MacOS) or `C:\Users\<Windows-username>\.kaggle\` (Windows)
5. **Warning**: Your Kaggle API key is readable by otherusers on this system! To fix this, you can run `chmod 600 /home/thi/.kaggle/kaggle.json`

## Download

If you wanna download some kaggle, you need to use something like that

~~~ bash
kaggle competitions download -c titanic
~~~

## Titanic - ML from disaster

### Understand problem

- There are 3 files: `train.csv` (data to train), `test.csv` (data to test and get the prediction), `gender_submission.csv` (just an example of file to be submitted after done)
- Use no matter what methods, try to predict who are the survivers, who are not in the `test.csv`

### Hint?

- You can find most of below hints in [titanic\#tutorial](https://www.kaggle.com/c/titanic#tutorials)
- Follow [ML course on kaggle](https://www.kaggle.com/learn/machine-learning), it says that this is place you can find everything needed for solving this kind of problem!
- Following [Titanic solution on python notebook](https://www.kaggle.com/startupsci/titanic-data-science-solutions) to understand at first!
- [ML from start to finish](https://www.kaggle.com/jeffd23/scikit-learn-ml-from-start-to-finish) using data from Titanic problem.
- Note that, there is [another one](https://triangleinequality.wordpress.com/2013/09/05/a-complete-guide-to-getting-0-79903-in-kaggles-titanic-competition-with-python/) (A complete guide to getting 0.79903 in Kaggle’s Titanic Competition with Python).


## Solution

- You can read my solutions/trying [here]({{site.baseurl}}/jupyter/titanic.html) (jupyter notebook).
