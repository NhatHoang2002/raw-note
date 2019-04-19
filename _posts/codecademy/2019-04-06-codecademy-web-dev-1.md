---
layout: post
title: "Codecademy - Web Development 1"
categories: [web]
tags: [html, codecademy web, codecademy]
toc: 1
comment: 1
date: 2019-04-08
---

This note is created when I started to learn the [Web Development path on Codecademy](https://www.codecademy.com/learn/paths/web-development).

## HTML

- Because the files are stored in the same folder, we can link web pages together using a relative path.
	~~~ 
	project-folder/
	|—— about.html
	|—— contact.html
	|—— index.html
	~~~
	
	~~~ html
	<a href="./contact.html">Contact</a>
	~~~
- A **relative path** is a filename that shows the path to a local file (a file on the same website, such as *./index.html*) 
- Which tag adds a new row header to an HTML table? `<th scope="row"></th>`. Without `scope`, we don’t know if it is for a row or a column.
- **Form**: in `<label for="meal">` and in `<input id="meal">`
	- **Input types**: [check here](https://www.w3schools.com/html/html_form_input_types.asp).
	- The `name` attribute specifies the name of an <input> element. 
		- The name attribute is used to **reference elements in a JavaScript**, or to reference form data **after a form is submitted**.
		- It's important to send info to other page when the form is submitted.
	- `required` attribute to **enforce** the user to type something before summiting the form.
	- `pattern="[0-9]{14,16}"`: regular expression (or regex)
	- `datalist` must have an input with the `list` attribute.
	- `select`: choose from given options, `datalist`: suggest some options but user can enter their options.

