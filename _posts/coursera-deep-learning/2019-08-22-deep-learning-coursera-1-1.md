---
layout: post
title: "DL Coursera 1 - NN & DL - W1: Intro 2 DL"
categories: [ml]
tags: [machine learning, deep-learning coursera, deep learning, coursera]
math: 1
toc: 1
comment: 1
date: 2019-08-31
---

{% assign img-url = '/images/posts/deep-learning-coursera' %}
{% assign lecture-url = '/files/DL-coursera' %}

This note was taken when I started to follow [the specialization Deep Learning](https://www.coursera.org/specializations/deep-learning) on Coursera. You can **audit** the courses in this specialization **for free**. In the case you wanna obtain a certification, you have to pay.

**Lectures in this week**: 

{% include toc.html %}

{% include more.html content="[Go to Week 2](/deep-learning-coursera-1-2)." %}

## Documentation

- [Beautifully drawn notes by Tess Ferrandez]({{lecture-url}}/picture-note-dl-coursera-tess.pdf "Drawn notes by Tess").
- **Next steps?**: Taking fast.ai courses series as it focuses more on the practical works ([ref](https://github.com/mbadry1/DeepLearning.ai-Summary)).  

## Welcome

- AI is the new electricity.
- Electricity had once transformed countless industries: transformation, manufacturing, healthcare, communications,...
- AI will now bring about an equally big transformation.
- **What you'll learn**:
  - (4 weeks) **Foundation: NN and DL**
    - How to build a new network / dl network & train it on data
    - Build a system to recognize cat! <-- **cat recognizer**
  - (3 weeks) **Improving Deep Neural Networks:**
    - Hyperparameters tuning
    - Regularization
    - Optimization: momentum armrest prop and the ad authorization algorithms.
  - (2 weeks) **Structuring your ML project**
    - It turns out that the strategy for building a machine learning system has changed in the era of deep learning.
    - train/test sets come from diff distributions <- frequently happen in DL
    - end-to-end DL (when should/shouldn't?)
  - **Convolutional Neural Networks** (CNNs)
    - usually applied to images!
  - **NLP** (building sequence models)
    - RNN
    - LSTM (Long Short Term Memory Model)
    - applied to speech recognition / music generation
    - NLP = sequence of words

## Introduction to Deep Learning

### What is a neural network?

- [Lecture notes]({{lecture-url}}/course-1/w1_What_is_Neural_Network_note.pdf) + [Lecture slides]({{lecture-url}}/course-1/w1_What_is_Neural_Network_ppt.pdf)
- Depp Learning = training Neural Networks (sometimes very large NN)
- Housing price prediction
  - Very simple NN: [ReLU function](https://en.wikipedia.org/wiki/Rectifier_(neural_networks)) (Rectified Linear Units)
    - y = price, x = size of house
  - Multiple NN:
  
    ![Multiple NN]({{img-url}}/multiple-nn-housing-price.jpg){:.no-border .w-600}
  
    - input layer - hidden layer - output layer
    - middle layer is **density connected** vì mọi inputs đều liên kết với mọi node trong middle layer (không giống cái hình ở trên là có những input không kết nối với các node trong middle layer)

### Supervised Learning with Neural Networks

- [Lecture notes]({{lecture-url}}/course-1/w1_Supervised_Learning_for_Neural_Network_note.pdf) + [Lecture slides]({{lecture-url}}/course-1/w1_Supervised_Learning_for_Neural_Network_ppt.pdf)
- all the economic value created by neural networks has been through **supervised learning**.
- 

### Why is Deep Learning taking off?

### About this course & Course Resources


