---
layout: post
title: "IBM Data Course 8: Machine Learning with Python (Week 4 to 6)"
categories: [data, python, ml]
tags: [data, ibm data, python, machine learning]
toc: 1
comment: 1
---

{% assign img-url = '/images/posts/data/ibm' %}

This note was first taken when I learnt the [IBM Data Professional Certificate course](https://www.coursera.org/specializations/ibm-data-science-professional-certificate) on Coursera.

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Course 8 (week 1 to 3)](/ibm-data-professional-certificate-8).
</span>
</div>

{% include more.html content="[Go to Course 9 (final course)](/ibm-data-professional-certificate-10)." %}

{% include toc.html %}

## Week 4: Clustering

### What's clustering?

- The important requirement is to use the available data to understand and identify **how customers are similar to each other**. Let's learn how to divide a set of customers into categories, based on characteristics they share.
- Clustering can group data <mark>only unsupervised</mark>, based on the similarity of customers to each other.
- Having this information would allow your company to develop highly personalized experiences for each segment.
- **Clustering** means finding clusters in a dataset, unsupervised.
- What's **difference between clustering and classification**?
  ![difference between clustering and classification]({{img-url}}/ibm-8-14.jpg){:.w-700}
- **Application of clustering**
  ![clustering application 1]({{img-url}}/ibm-8-15.jpg){:.w-500}
  ![clustering application 2]({{img-url}}/ibm-8-16.jpg){:.w-500}
- **Why clustering?**
  - Exploratory data analysis
  - Summary generation
  - Outlier detection
  - Finding duplicates
  - Pre-processing steps
- **Clustering algorithms**
  - *Partitioned-based clustering*
    - Relatively efficient
    - eg. K-means, k-median, fuzzy c-means
    - used for medium or large size databases
  - *Hierarchical clustering*
    - produces trees of clusters
    - eg. agglomerative, divisive
    - very intuitive
    - good for small size dataset
  - *Density-based clustering*
    - produces arbitary shaped clusters
    - eg. DBSCAN
    - used for special cluster or there is noise in your dataset

### k-Means Clustering

- 




