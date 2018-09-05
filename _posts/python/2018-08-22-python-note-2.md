---
layout: post
title: "Python 2 : Tricks"
categories: it
tags: [python]
maths: 1
toc: 1
date: 2018-08-22
datacamp: 1
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
