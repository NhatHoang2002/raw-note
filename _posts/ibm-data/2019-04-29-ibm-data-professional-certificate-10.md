---
layout: post
title: "IBM Data Course 9: Applied Data Science Capstone"
categories: [data, python, ml]
tags: [data, ibm data, python, machine learning]
toc: 1
comment: 1
date: 2019-05-02
---

{% assign img-url = '/images/posts/data/ibm' %}

This note was first taken when I learnt the [IBM Data Professional Certificate course](https://www.coursera.org/specializations/ibm-data-science-professional-certificate) on Coursera.

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Course 8 (week 4 to 6)](/ibm-data-professional-certificate-9).
</span>
</div>

{% include toc.html %}

## Week 1 : Introduction to Capstone Project

- You live on the west side of the city of Toronto in Canada. You love your neighborhood
  - Now say you receive a job offer from a great company **on the other side**. 
  - However given the **far distance from your current** place 
  - You must move if you decide to accept the offer. 
  - The neighborhoods on the other side of the city that are exactly the same as your current neighborhood? and if not perhaps similar neighborhoods that are at least closer to your new job? 
- Name : **Battle of the neighborhoods**
- **Jobs**:
  - **Segment** a city into different neighborhoods using the **geographical coordinates** of the center of each neighborhood.
  - Using a combination of location data and machine learning, you will **group the neighbourhoods into clusters**
- **5 modules**
  - Module 1 to 3: learn additional skills.
  - Module 4 & 5: the project.

### Location Data Providers

- **Location data** is data describing places and venues, such as their geographical location, their category, working hours, full address, and so on, such that for a given location given in the form of its geographical coordinates (or latitude and longitude values) one is able to determine what types of venues exist within a defined radius from that location.
  ![Example of location data]({{img-url}}/ibm-9-1.jpg)
- **Location data provider**: Foursquare, Google places, Yelp
  - **Rate limit**: How many API calls you can make (per hour, per day)
  - **Cost**: How much does it cost?
  - **Coverage**: how many countries or geographical locations the location data set covers. 
  - **Accuracy**: how accurate is the location data provided
  - **Update frequecy**: How often the data are updated?
- In this project, we use **[Foursquare](https://foursquare.com/)**.
- [My assignment](https://github.com/dinhanhthi/Coursera_Capstone): create a repository with a jupyter notebook on Github.

## Week 2 : Foursquare API

### Introduction to Foursquare

- **accurate** location data.
- Apple maps, uber, snapchat, twitter,...
- [Create an account on FS](https://foursquare.com/developers/).

### Using Foursquare API

<div class="columns-2" markdown="1">
![API-search]({{img-url}}/ibm-9-2.jpg)

![API-search 2]({{img-url}}/ibm-9-3.jpg)
</div>

<div class="columns-2" markdown="1">
![API-search 3]({{img-url}}/ibm-9-4.jpg)

![API-search 4]({{img-url}}/ibm-9-5.jpg)
</div>


