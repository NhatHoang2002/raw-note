---
layout: post
title: "Secure and Private AI Scholarship Challenge: PyTorch"
categories: [ml]
tags: [machine learning]
math: 1
toc: 1
comment: 1
---

{% assign img-url = '/images/posts/ML/ai-challenge' %}
{% assign jupyter-url = '/files/ai-challenge' %}

This note was first taken when I learnt the [Secure and Private AI Scholarship Challenge](https://eu.udacity.com/facebook-AI-scholarship) on Udacity.

{% include toc.html %}

{% include more.html content="[Go to Part 2](/secure-and-private-ai-scholarship-challenge-2)." %}

## About PyTorch

- [Official website of PyTorch](https://pytorch.org/).
- Released in 2017 + deep learning + by facebook.
- By the end of this lesson: 
  - Using deep learning to *classify images of cats and dogs*.
  - Next, define a loss and an optimization method to train the neural network on a dataset of *handwritten digits*.
  - how to test that your network is able to generalize through **validation**.
  - **transfer learning**: how to use pre-trained networks to improve the performance of your classifier.
- **tensors** - the main data structure of PyTorch.
- **autograd** : a module called that PyTorch uses to calculate gradients for training neural networks.
- PyTorch uses a library called **[CUDA](https://developer.nvidia.com/cuda-zone)** to accelerate operations using the GPU

## Single layer neural networks

<p markdown="1" class="thi-tip">
<i class="material-icons mat-icon">info</i>
[Jupyter notebook Part 1 - Tensors in PyTorch]({{jupyter-url}}/Part 1 - Tensors in PyTorch (Exercises).html).
</p>

- **[PyTorch](http://pytorch.org/)** in a lot of ways behaves like the arrays you love from Numpy. These Numpy arrays, after all, are just **tensors**. 
  - PyTorch takes these tensors and makes it simple to move them to GPUs for the faster processing needed when training neural networks.
  - It also provides a module that automatically calculates gradients (for backpropagation!) and another module specifically for building neural networks. 
- It turns out **neural network computations are just a bunch of linear algebra operations on tensors**, a generalization of matrices. A vector is a 1-dimensional tensor, a matrix is a 2-dimensional tensor, an array with three indices is a 3-dimensional tensor (RGB color images for example). 

  ~~~ python
  # First, import PyTorch
  import torch
  
  def activation(x):
    """ Sigmoid activation function 
    
        Arguments
        ---------
        x: torch.Tensor
    """
    return 1/(1+torch.exp(-x))
  
  ### Generate some data
  torch.manual_seed(7) # Set the random seed so things are predictable
  
  # Features are 3 random normal variables
  features = torch.randn((1, 5))
  # True weights for our data, random normal variables again
  weights = torch.randn_like(features)
  # and a true bias term
  bias = torch.randn((1, 1))
  ~~~

- In general, you'll use **PyTorch tensors pretty much the same way you'd use Numpy arrays**.
  - PyTorch tensors come with some nice benefits though such as GPU acceleration.
- Check the shape of some tensor, called `ts`: `ts.shape`
- Reshape a tensor: `ts.reshape(a,b)`
- Resize a tensor: `ts.resize(a,b)` or `ts.resize_(a,b)` (the underscore makes **in-place**) or `ts.view(a,b)`
- [Inplace operations in PyTorch](https://discuss.pytorch.org/t/what-is-in-place-operation/16244).
- Taking sum: `torch.sum()` or `ts.sum()`
- **Matrix multiplication**: `torch.mm()` or `torch.matmul()`

  ~~~ python
  ## Calculate the output of this network using matrix multiplication
  y = activation( torch.mm(features, weights.view(5,1)) + bias )
  ~~~

- Stack them up! (There is hidden layer)

  ~~~ python
  ### Generate some data
  torch.manual_seed(7) # Set the random seed so things are predictable
  
  # Features are 3 random normal variables
  features = torch.randn((1, 3))
  
  # Define the size of each layer in our network
  n_input = features.shape[1]     # Number of input units, must match number of input features
  n_hidden = 2                    # Number of hidden units 
  n_output = 1                    # Number of output units
  
  # Weights for inputs to hidden layer
  W1 = torch.randn(n_input, n_hidden)
  # Weights for hidden layer to output layer
  W2 = torch.randn(n_hidden, n_output)
  
  # and bias terms for hidden and output layers
  B1 = torch.randn((1, n_hidden))
  B2 = torch.randn((1, n_output))
  
  ## Your solution here
  h = activation(torch.mm(features, W1) + B1)
  y = activation(torch.mm(h, W2) + B2)
  y
  ~~~

- From **numpy** to **PyTorch**: `torch.from_numpy()`
  - numpy --> array, pytorch --> tensor
- From pytorch to numpy: `ts.numpy()`
- <mark>The memory is shared between the Numpy array and Torch tensor</mark>, so if you change the values in-place of one object, the other will change as well.

## Neural Networks in PyTorch

<p markdown="1" class="thi-tip">
<i class="material-icons mat-icon">info</i>
[Jupyter notebook Part 2 - Neural networks with PyTorch]({{jupyter-url}}/Part 1 - Tensors in PyTorch (Exercises).html).
</p>

- Deep learning networks tend to be massive with dozens or hundreds of layers, that's <mark>where the term "deep" comes from.</mark> 
- The networks you've seen so far are called **fully-connected** or **dense networks**. *Each unit in one layer is connected to each unit in the next layer.* 
  - In fully-connected networks, the input to each layer must be a one-dimensional vector (which can be stacked into a 2D tensor as a batch of multiple examples). 
  - Thinking about sizes, we need to convert the batch of images with shape `(64, 1, 28, 28)` to a have a shape of `(64, 784)`, 784 is 28 times 28. This is typically called **flattening**, we flattened the 2D images into 1D vectors.
- **Softmax function**. What this does is squish each input $x\_i$ between 0 and 1 and normalizes the values to give you a proper probability distribution where the probabilites sum up to one.
  $$
  \Large \sigma(x_i) = \cfrac{e^{x_i}}{\sum_k^K{e^{x_k}}}
  $$
- `torch.sum(dim=0)`: Setting `dim=0` takes the sum across the rows while `dim=1` takes the sum across the columns.

  ~~~ python
  # x's shape is 64x10
  def softmax(x):
      return x/torch.sum(x,dim=1).view(64,1)
  ~~~

- Using `torch.nn` to build a neural network

~~~ python
from torch import nn

class Network(nn.Module): # Here we're inheriting from nn.Module
  def __init__(self):
    super().__init__()
    
    # Inputs to hidden layer linear transformation
    self.hidden = nn.Linear(784, 256)
    # Output layer, 10 units - one for each digit
    self.output = nn.Linear(256, 10)
    
    # Define sigmoid activation and softmax output 
    self.sigmoid = nn.Sigmoid()
    self.softmax = nn.Softmax(dim=1)
      
  def forward(self, x):
    # Pass the input tensor through each of our operations
    x = self.hidden(x)
    x = self.sigmoid(x)
    x = self.output(x)
    x = self.softmax(x)
    
    return x
~~~

  or other common way,

  ~~~ python
  import torch.nn.functional as F
  
  class Network(nn.Module):
    def __init__(self):
      super().__init__()
      # Inputs to hidden layer linear transformation
      self.hidden = nn.Linear(784, 256)
      # Output layer, 10 units - one for each digit
      self.output = nn.Linear(256, 10)
        
    def forward(self, x):
      # Hidden layer with sigmoid activation
      x = F.sigmoid(self.hidden(x))
      # Output layer with softmax activation
      x = F.softmax(self.output(x), dim=1)
      
      return x
  ~~~

- So far we've only been looking at the softmax activation, but in general any function can be used as an activation function. The only requirement is that for a network to approximate a non-linear function, <mark>the activation functions must be non-linear</mark>. 