---
title: "Codecademy - Python 1"
categories: [python]
tags: [python, codecademy python, codecademy]
toc: 1
comment: 1
---

This note is created when I started to learn the [Learn Python 3](https://www.codecademy.com/courses/learn-python-3) on Codecademy.

## Basic

- Multiplines string
	~~~ python
	leaves_of_grass = """
	Poets to come! orators, singers, musicians to come!
	Not to-day is to justify me and answer what I am for,
	But you, a new brood, native, athletic, continental, greater than
	  before known,
	Arouse! for you must justify me.
	"""
	~~~
- To pass variables to a function, there are 2 ways: *positional arguments* (1st value for the 1st arg,...) and *keyword arguments* (with the keywords)
- We can define a default keyword like this
	~~~ python
	def greet_customer(special_item, grocery_store="Engrossing Grocers"):
	    print("Welcome to "+ grocery_store + ".")
	    print("Our special is " + special_item + ".")
	    print("Have fun shopping!")
	~~~
- Multiple return values
~~~ python
def square_point(x_value, y_value):
  x_2 = x_value * x_value
  y_2 = y_value * y_value
  return x_2, y_2
~~~



