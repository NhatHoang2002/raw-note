---
layout: post
title: "Onogone's test"
categories: [ml, data]
tags: [machine learning, data, interview]
maths: 1
toc: 1
---

All things I've learned from the test of Onogone company.

## Useful links

- [Practical Text Classification With Python and Keras](https://realpython.com/python-keras-text-classification/) : good explanation!

## Definition

- **Baseline model** : This usually involves a simple model, which is then used as a comparison with the more advanced models that you want to test.

## How to predict?

- Count the frequency of each word
- 

## Cound the frequency of each word

Building a vocabulary

~~~ python
from sklearn.feature_extraction.text import CountVectorizer

sentences = ['John likes ice cream', 'John hates chocolate.', "Thi likes butter", "Thi hates chocolate."]

vectorizer = CountVectorizer(min_df=0, lowercase=False)
vectorizer.fit(sentences)

print(vectorizer.vocabulary_)
~~~

