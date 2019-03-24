---
title: "IBM Data Course 2: Open Source tools for Data Science - Week 1-2-3"
categories: [data]
tags: [data, ibm data]
toc: 1
comment: 1
---

{% assign img-url = '/images/posts/data/ibm' %}

This note was first taken when I learnt the [IBM Data Professional Certificate course](https://www.coursera.org/specializations/ibm-data-science-professional-certificate) on Coursera.

{% include toc.html %}

{% include more.html content="[Go to Week 2](/machine-learning-coursera-2)." %}

## Week 1

### Cognitive Class Labs

- **What is [Cognitive Class Labs?](https://labs.cognitiveclass.ai/)**
	- Online platform/web service for AI, Data with already-built tools (notebooks, rstudio ide, openrefine,...)
	- Jupyter Notebook (before is IPython Notebooks)
	- Rstudio with Shiny enables you to create interactive apps or visualizations.
	- Zeppelin Notebook contains basic charts which allows you to convert data tables directly into visualizstions without any code.
	- Seahorse (workflow)
- Create an account at [https://labs.cognitiveclass.ai/](https://labs.cognitiveclass.ai/)
- **Managing data within My Data**.
	- can upload any filetype

### Jupyter Notebooks

- **JupyerLab** : environment contains juyter notebooks.
- **JupyerNotebook** : actual file.
- in Jupyter notebooks, you can only use **one language at a time**.

## Week 2

### Zeppelin Notebooks

- Come with the following built in: Apache Spark, certain data visualizations and pivot charts.
- You can use multiple programming languages in the same Zeppelin notebook, e.g. Scala + SQL. This is one of the key **differences between Jupyter and Zeppelin notebooks**; in Jupyter notebooks, you can only use one language at a time.
- Each paragraph can be columned like in bootstrap.
- file type of Zeppelin notebook: **JSON**

### RStusio IDE

- **Shiny** to create interactive code.
- Only for programming in R.
- The reason why 'sc' is one of the default variables in RStudio IDE on Cognitive Class Labs is because: "sc" stands for "SparkContext" and is created by default to enable users to use Apache Spark from RStudio IDE.

## Week 3

### IBM Watson Studio

<p markdown="1" class="thi-warning">
<i class="material-icons mat-icon">error</i>
**IBM Watson Studio** and **Cognitive Class Labs** are different! (different accounts to sign in)
</p>

IBM Watson Studio, formerly known as *Data Science Experience* or DSX, in an enterprise-ready environment for data scientists and developers, and includes some of the tools as you have learned so far on Cognitive Class Labs. You may find that many of the features are similar as what you have seen on Cognitive Class Labs. However, because IBM Watson Studio was designed for scalability and enterprise usage, you will find some extra features that include (1) collaboration with team members, (2) scalability with Spark clusters to analyze big data, and (3) connections to various data sources.

IBM Watson Studio also comes with a free trial, which includes Jupyter Notebooks, RStudio, space for object storage, 2 Spark executors, and a community that includes notebooks and tutorials that you can use.

Note that the videos in this course may still include references to "Data Science Experience" or "DSX", but in your mind, simply replace those terms with "Watson Studio". Thank you for your patience with us as we update the videos!

- **You can register for IBM Watson Studio here**: [https://cloud.ibm.com/catalog/services/watson-studio](https://cloud.ibm.com/catalog/services/watson-studio)
- Jupyter Notebook and RStudio are both available on IBM Data Science.
- 



