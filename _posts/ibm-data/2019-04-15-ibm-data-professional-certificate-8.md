---
title: "IBM Data Course 8: Machine Learning with Python"
categories: [data, python, ml]
tags: [data, ibm data, python, machine learning]
toc: 1
comment: 1
math: 1
---

{% assign img-url = '/images/posts/data/ibm' %}

This note was first taken when I learnt the [IBM Data Professional Certificate course](https://www.coursera.org/specializations/ibm-data-science-professional-certificate) on Coursera.

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Course 7](/ibm-data-professional-certificate-7).
</span>
</div>

{% include more.html content="[Go to Course 9 (final of the series)](/ibm-data-professional-certificate-9)." %}

{% include toc.html %}

## Week 1: Introduction to Machine Learning

- **What is ML?** Machine learning is the subfield of computer science that gives "computers the ability to learn without being explicitly programmed."
- **Major ML techniques**: 
	- *Regression / Estimation*: predicting continuous values -> Predicting price of the house based on charateristics
	- *Classification*: Predicting item class/category of a case -> If a cell is benign or malignant
	- *Clustering*: Finding the structure of data / summarization ->  can find similar patients, or can be used for customer segmentation in the banking field.
	- *Association*: Associating frequent co-occuring items/events -> grocery items that are usually bought together by a particular customer. 
	- *Anomaly detection*: Discovering abnormal and unusual cases -> it is used for credit card fraud detection.
	- *Sequence mining*: Predicting next events, click-stream (Markov Model, HMM) -> the click-stream in websites.
	- *Dimension Reduction*: Reducing the size of data (PCA)
	- *Recommendation systems*: Recommending items -> associates people's preferences with others who have similar tastes, and recommends new items to them, such as books or movies.
- **ML vs AI vs Deep Learning**: 
	- AI: make computer smarter like a human (computer vision, language processing, creativity,...)
	- ML: a branch of AI. It teaches computer to solve problems, learning from thousands of examples to solve the same problem in new situations.
	- Deep Learning: a special case of ML where computer learn and make intelligent decisions on their own.
- **Python for ML**: 
	- **numpy**: is a math library to work with N-dimensional arrays in Python. It enables you to do computation efficiently and effectively. 
	- **scipy**: is a collection of numerical algorithms and domain specific toolboxes, including signal processing, optimization, statistics and much more. SciPy is a good library for scientific and high performance computation. 
	- **Matplotlib**: provides 2D plotting, as well as 3D plotting.
	- **Pandas**: provides high performance easy to use data structures. It has many functions for data importing, manipulation and analysis. In particular, it offers data structures and operations for manipulating *numerical tables* and *timeseries*.
	- **scikitlearn**: a collection of algorithms and tools for machine learning.  
		- It has most of the classification, regression and clustering algorithms, and it's designed to work with a Python numerical and scientific libraries; NumPy and SciPy. 
		- Most of the tasks that need to be done in a machine learning pipeline are implemented already in Scikit Learn including pre-processing of data, feature selection, feature extraction, train test splitting, defining the algorithms, fitting models, tuning parameters, prediction, evaluation and exporting the model. 
- **Supervised vs Unsupervised**
	- **Supervsised learning**: means to observe, and direct the execution of a task, project, or activity.
		- We teach the model by training it with some data from a labeled dataset. 
		- 2 types: classification vs regression
		- deal with labeled data
	- **unsupervised learning**: is exactly as it sounds. We do not supervise the model, but we let the model work on its own to discover information that may not be visible to the human eye.
		- unsupervised learning has more difficult algorithms than supervised learning since we know little to no information about the data, or the outcomes that are to be expected.
		- clustering
		- deal with unlabeled data

## Week 2: Regression

<p markdown="1" class="thi-tip">
<i class="material-icons mat-icon">info</i>
- Check [the lab: simple linear regression]({{site.baseurl}}/files/ibm/ML0101EN-Reg-Simple-Linear-Regression-Co2-py-v1.html) for the example and guide.
- [the lab: multiple linear regression]({{site.baseurl}}/files/ibm/ML0101EN-Reg-Mulitple-Linear-Regression-Co2-py-v1.html)
- [the lab: polynomial regression]({{site.baseurl}}/files/ibm/ML0101EN-Reg-Polynomial-Regression-Co2-py-v1.html)
- - [the lab: non-linear regression]({{site.baseurl}}/files/ibm/ML0101EN-Reg-NoneLinearRegression-py-v1.html)
</p>

### Linear regression

- The key point in the regression, is that our dependent value **should be continuous**, and cannot be a discrete value. -> **quantity**
- 2 **types** of regressions: 
	- simple regression: linear/non-linear regression
	- multiple regression: multiple linear/non-linear regression
- **Examples**:
	- Sales forecasting
	- Sastisfaction analysis
	- Price estimation
	- Employment income
- **Algorithms**
	- Ordinal regression 
	- Poisson regression
	- Fast forest quantile regression
	- Linear, Polynomial, Lasso, Stepwise, Ridge regression
	- Bayesian network regression
	- Decision forest regression
	- Boosted decision tree regression
	- KNN (K-nearest neighbors)
- **Training accuracy**: is the percentage of correct predictions that the model makes when using the test dataset.
	- High training accuracy is not a good thing -> may overfitting!
- **Out-of-sample accuracy** is the percentage of correct predictions that the model makes on data that the model has not been trained on. 
	- It's important that our models have high out-of-sample accuracy
	- Highly dependent on which dataset the data is trained and tested.
- **K-fold cross-validation**: K-fold cross-validation in its simplest form performs multiple train/test splits, using the same dataset where each split is different.
	![K-fold cross-validation]({{img-url}}/ibm-8-1.jpg){:.w-700}
- **Errors metrics**: the higher $R^2$, the better your model fit your data.
	![Type of errors]({{img-url}}/ibm-8-2.jpg){:.w-700}
- **Multiple regression**
	- First, it can be used when we would like to identify the strength of the effect that the independent variables have on the dependent variable.
	- Second, it can be used to predict the impact of changes, that is, to understand how the dependent variable changes when we change the independent variables.
	- Using many variables -> overfitting
	- Using scatter plot to check if there is a linear regression. If not, use non-linear regression.
- **Ordinary Least Squares** (OLS): OLS is a method for estimating the unknown parameters in a linear regression model. OLS chooses the parameters of a linear function of a set of explanatory variables by minimizing the sum of the squares of the differences between the target dependent variable and those predicted by the linear function. In other words, it tries to minimizes the sum of squared errors (SSE) or mean squared error (MSE) between the target variable (y) and our predicted output ($\hat{y}$) over all samples in the dataset.
	- Solving the model parameters analytically using closed-form equations
    - Using an optimization algorithm (Gradient Descent, Stochastic Gradient Descent, Newton’s Method, etc.)

### Non-linear regression

- **What**: First, non-linear regression is a method to model a non-linear relationship between the dependent variable and a set of independent variables. Second, for a model to be considered non-linear, Y hat must be a non-linear *function of the parameters Theta*, *not necessarily the features *X.
	$$
	\hat{y} = \theta_0 + \theta_1\theta_2^x
	$$
- **Polynomial regression**: 
	- Polynomial regression fits a curve line to your data.
	- a polynomial regression model can still be expressed as linear regression. 
	- Therefore, polynomial regression models can fit using the model of least squares. **Least squares** is a method for estimating the unknown parameters in a linear regression model by minimizing the sum of the squares of the differences between the observed dependent variable in the given dataset and those predicted by the linear function.

## Week 3: Classification

<mark>NEED TO BE NOTED LATER!!!!</mark>

<p markdown="1" class="thi-tip">
<i class="material-icons mat-icon">info</i>
Labs
- [KNN]({{site.baseurl}}/files/ibm/ML0101EN-Clas-K-Nearest-neighbors-CustCat-py-v1.html)
- [Decision Trees]({{site.baseurl}}/files/ibm/ML0101EN-Clas-K-Nearest-neighbors-CustCat-py-v1.html)
</p>

- Supervised learning approaches.
- **Multiclass classifier**: A classifier that can predict a field with multiple discrete values, such as "DrugA", "DrugX" or "DrugY".
- 