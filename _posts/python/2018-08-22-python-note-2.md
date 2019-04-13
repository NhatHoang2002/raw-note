---
layout: post
title: "Python 2 : Tricks"
categories: [it, python]
tags: [python]
maths: 1
toc: 1
date: 2018-09-18
comment: 1
---

I use this note for only tricks in Python (quick exercises solution also).

## Check string

- Check ASCII

    ~~~ python
    is_ascii = lambda s: len(s) == len(s.encode())
    ~~~

- Check there is any digit numbers?

    ~~~ python
    has_digit = lambda s: any(char.isdigit() for char in s)
    ~~~

- `s.isupper()`, `s.islower()`

## List

- Delete all same element 'a' from list

  ~~~ python
  arr = [x for x in arr if x != 'a']
  ~~~

  Note that, if we only want to delete 1 element a, use `arr.remove('a')`

- Remove duplicates and only keep 1 of them: change to `set`: `b = set(a)` where `a` is a list
