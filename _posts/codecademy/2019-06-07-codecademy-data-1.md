---
layout: post
title: "Codecademy - Data Science 1"
categories: [data]
tags: [data, data codecademy, codecademy]
comment: 1
toc: 1
date: 2019-07-24
---

{% assign img-url = '/images/posts/codecademy/data' %}

This note is created when I started to learn the [Data Science](https://www.codecademy.com/paths/data-science) on Codecademy.

## A day in life - Data Analyst

- Data extraction with SQL
- Programming basics with Python
- Data analysis using pandas, a Python library
- Data visualization using Matplotlib, a Python library
- Machine Learning using scikit-learn, a Python library

## Relational Database Management System (RDMS)

- RDBMS use **SQL** language to access the database.
- Popular RDBMS: 
  - **SQLite**: 
    - all of the data can be stored locally
    - popular choice for databases in cellphones, PDAs, MP3 players, set-top boxes, and other electronic gadgets. <mark>The SQL courses on Codecademy use SQLite.</mark>
  - **MySQL**:
    - the most popular open source SQL database
    - easy to use, inexpensive, reliable, large community of developers
    - poor performance when scaling, open source development has lagged 
    - does not include some advanced features that developers may be used to
  - **PostgreSQL**:
    - open source SQL database
    - shares many of the same advantages of MySQL
    - foreign key support without requiring complex configuration.
    - slower in performance than other databases
  - **Oracle DB**:
    - not open sourced (Oracle Corporation owns)
    - for large applications, particularly in the banking industry
  - **SQL Server**:
    - Microsoft owns
    - Large enterprise applications mostly use SQL Server.
    - offers a free entry-level version called Express

## SQL

- **[Just look up at this site](https://www.w3schools.com/sql/sql_delete.asp)**!
- `ALTER TABLE` statement adds a new column to a table. 

  ~~~ sql
  ALTER TABLE celebs 
  ADD COLUMN twitter_handle TEXT;
  ~~~

- **Constraints** that add information about how a column can be used are invoked after specifying the data type for a column.

  ~~~ sql
  CREATE TABLE celebs (
     id INTEGER PRIMARY KEY, 
     name TEXT UNIQUE,
     date_of_birth TEXT NOT NULL,
     date_of_death TEXT DEFAULT 'Not Applicable'
  );
  ~~~

- `AS`

  ~~~ sql
  SELECT name AS 'ten'
  FROM movies;
  ~~~

- `DISTINCT` is used to return unique values in the output. It filters out all duplicate values in the specified column(s).
- `LIKE` can be a useful operator when you want to compare similar values. Check [this](https://www.w3schools.com/sql/sql_like.asp) for other usesages.
- A `CASE` statement allows us to create different outputs (usually in the SELECT statement). It is SQL’s way of handling if-then logic.
- [Cross join](https://www.w3resource.com/sql/joins/cross-join.php)
- `with` statements

  ~~~ sql
  WITH previous_results AS (
     SELECT ...
     ...
     ...
     ...
  )
  SELECT *
  FROM previous_results
  JOIN customers
    ON _____ = _____;
  ~~~


## Numpy with Statistics

- `np.percentile(d, 40)` gives the number which divides array `d` into 40% and 60%.
- **histogram**:

  ~~~ python
  plt.hist(commutes, range=(20,50), bins=6)
  ~~~

- A **unimodal dataset** has only one distinct peak. (1 đỉnh)
- A **bimodal dataset** has two distinct peaks. This often happens when the data contains two different populations. (2 đỉnh)
- A **multimodal dataset** has more than two peaks.
- A **uniform dataset** doesn’t have any distinct peaks.
- A **symmetric dataset** has equal amounts of data on both sides of the peak. Both sides should look about the same.
- A **skew-right dataset** has a long tail on the right of the peak, but most of the data is on the left.
- A **skew-left dataset** has a long tail on the left of the peak, but most of the data is on the right.
- <mark>The type of distribution affects the position of the mean and median</mark>. In heavily skewed distributions, the mean becomes a less useful measurement.
- the **normal distribution**, which is a symmetric, unimodal distribution.
- **random number generator** (fit a normal distribution):
  - `a = np.random.normal(loc=0, scale=1, size=100000)`
  - `loc` (mean of normal dist), `scale` (SD of ND), `size` (# of random numbers)
- We expect that **68%** of our dataset to be between [mean-std, mean+std]
  - 68% of our samples will fall between +/- 1 standard deviation of the mean
  - 95% of our samples will fall between +/- 2 standard deviations of the mean
  - 99.7% of our samples will fall between +/- 3 standard deviations of the mean
- **The binomial distribution** can help us. It tells us how likely it is for a certain number of “successes” to happen, given a probability of success and a number of trials.
  - The binomial distribution is important because it allows us to know <mark>how likely a certain outcome is, even when it’s not the expected one.</mark>
  - Exp: 70% số người mua vị gà (70 trong 100 người sẽ chọn gà) nhưng khả năng "7 trong 10 người chọn gà" thì rất thấp (27% mà thôi).
  - `np.random.binomial(10, 0.30, size=10000)`

  ~~~ python
  # Our basketball player has a 30% chance of making any individual basket. He took 10 shots and made 4 of them, even though we only expected him to make 3. What percent chance did he have of making those 4 shots?
  
  a = np.random.binomial(10, 0.30, size=10000)
  np.mean(a == 4)
  # 0.1973

  # 2nd way
  len(a[a==4]) / len(a)
  ~~~

## Hypothesis Testing (SciPy)

- [Link course](https://www.codecademy.com/paths/data-science/tracks/scipy).
- **engagement** -> time people spend on your website.
- Performing an **A/B test** — are the different observations really the results of different conditions (i.e., Condition A vs. Condition B)? Or just the result of random chance?
- **Conducting a survey** — is the fact that men gave slightly different responses than women a real difference between men and women? Or just the result of chance?
- The individual measurements on Monday, Tuesday, and Wednesday are called **samples**. A sample is a subset of the **entire population**. The mean of each sample is the **sample mean** and it is an estimate of the **population mean**.
- **Central Limit Theorem**: 
  - Sometime, you measured more one sample than the others. That makes your sample selection skewed to one direction of the total population.
  - if we have a large enough sample size, all of our sample means will be sufficiently close to the population mean.
- **Hypothesis Tests**: 
  - Hypothesis testing is a mathematical way of determining *whether we can be confident that the null hypothesis is false*.
  - **null hypothesis** ($H\_0$): *the null hypothesis is the proposition that there is no effect or no relationship between phenomena or populations.* ([ThoughtCo](https://www.thoughtco.com/definition-of-null-hypothesis-and-examples-605436))
  - Chúng ta có thể test các null hypothesis này để thấy rằng chúng có thể sai mà từ đó thấy được mối quan hệ của các thành phần.
  - **The alternate hypothesis** ($H\_A$ or $H\_1$)
  - **Example** (*How to State a Null Hypothesis?*): Mối liên quan giữa số lần tập thể dục mỗi tuần và số kg giảm được. Giả sử mỗi tuần tập 5 lần sẽ giảm 6kg. Bây giờ ta giảm số lần tập mỗi tuần xuống còn 3 thì liệu số kg giảm được sẽ ít hơn 6 ko?
    - $H\_A=H\_1=\{ \mu<6 \}$ (Alternate hypothesis)
    - $H\_0 = \{ \mu\ge 6 \}$ (chẳng những không giảm mà còn tăng)
    - Cách biểu diễn khác: $H\_0 = \{ \mu = 6 \}$ (giảm số lần tập cũng không ảnh hưởng đến số kg giảm)
  - **Other example**:
    - "Hyperactivity is unrelated to eating sugar" (Tăng động không liên quan đến ăn đường) is an example of a null hypothesis.
  - **Type I** = False Positive, **Type II** = False Negative. Check [my article](https://dinhanhthi.com/understand-confusion-matrix-and-f1-score) about Confusion matrix.
    - Type I = **FP** = the null hypothesis is **rejected** even though it is true.
    - Type II = **FN** = the null hypothesis is **accepted** even though it is false.
- **P-Values**: A hypothesis test provides a numerical answer, called a p-value, that helps us decide how confident we can be in the result.
  - a p-value is the probability that we yield the observed statistics under the assumption that the null hypothesis is true.
  - **Example**: A p-value of 0.05 would mean that there is a 5% chance that there is no difference between the two population means.
  - A **higher** p-value is more likely to give a FP so if we want to be very sure that the result is not due to just chance, we will select a very small p-value.




