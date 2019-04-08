---
title: "Codecademy - Web Development 1"
categories: [web]
tags: [html]
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

