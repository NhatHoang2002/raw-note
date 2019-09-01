---
layout: post
title: "DL Coursera 1 - NN & DL - W1: Intro to DL"
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
    - Build a system to recognize cat! <-- **<mark>recognize a cat</mark>**
  - (3 weeks) **Improving Deep Neural Networks:**
    - Hyperparameters tuning
    - Regularization
    - Optimization: momentum armrest prop and the ad authorization algorithms.
  - (2 weeks) **Structuring your ML project**
    - It turns out that the strategy for building a machine learning system has changed in the era of deep learning.
    - train/test sets come from diff distributions <- frequently happen in DL
    - end-to-end DL (when should/shouldn't?)
  - **Convolutional Neural Networks** (<mark>CNNs</mark>) [*convolutional: tính chập*]
    - usually applied to images!
  - **NLP** (building <mark>sequence models</mark>)
    - <mark>RNN</mark> (Recurrent Neural Network) <-- nếu sequence data thì thường dùng cái này!
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
    - input layer - hidden layer - output layer
    - middle layer is **density connected** vì mọi inputs đều liên kết với mọi node trong middle layer (không giống cái hình ở trên là có những input không kết nối với các node trong middle layer)
    
    ![Multiple NN]({{img-url}}/multiple-nn-housing-price.jpg){:.no-border .w-600}

### Supervised Learning with Neural Networks

- [Lecture notes]({{lecture-url}}/course-1/w1_Supervised_Learning_for_Neural_Network_note.pdf) + [Lecture slides]({{lecture-url}}/course-1/w1_Supervised_Learning_for_Neural_Network_ppt.pdf)
- all the economic value created by neural networks has been through **supervised learning**.

<div class="row d-flex" markdown="1">
<div class="col s12 l5" markdown="1">
![Supervised Learning with DL]({{img-url}}/c1-w1-1.jpg){:.no-border}
</div>
<div class="col s12 l7" markdown="1">
![Illustration for some DL algorithms]({{img-url}}/c1-w1-2.jpg){:.no-border}
</div>
</div>

- Supervised Learning: structured data vs unstructured data
  - **structured data**: each of feature has a very well defined meaning.
  - **unstructured data**: audio, images, words in text <-- thanks to NN, DL, computers are now much better at interpreting this type of data.

### Why is Deep Learning taking off?

- [Lecture notes]({{lecture-url}}/course-1/w1_Why_is_Deep_Learning_Taking_Off_note.pdf) + [Lecture slides]({{lecture-url}}/course-1/w1_Why_is_Deep_Learning_Taking_Off_ppt.pdf)
- Tại sao ý tưởng của DL có từ lâu mà tới giờ nó mới phát triển thật sự như vậy?

  ![Scale drives DL progress]({{img-url}}/c1-w1-2.jpg){:.no-border .w-600}

- If you wanna hit a very high performance, you need 2 conditions:
  - **train a bigger network**: train a big enough NN in order to take advantage of the huge amount of data <-- take to long to train
  - **throw more data at it**: you do need a lot of data <-- we often don't have enough data
- **Scale** drives DL progress:
  - Data
  - Computation (CPU, GPU)
  - Algorithms
    - Ex: changing from sigmoid function to ReLU function make faster
  - The process of training a NN is iterative (Idea> Code > Experiment > Idea ...): faster computation helps to iterate and improve new algorithm.

### About this course & Course Resources

- **Week 1**: Introduction
- **W2**: Basics of NN programming
- **W3**: One hidden layer NN
- **W4**: Deep NN

### Geoffrey Hinton interview

- [Geoffrey Hinton from wiki](https://en.wikipedia.org/wiki/Geoffrey_Hinton).


