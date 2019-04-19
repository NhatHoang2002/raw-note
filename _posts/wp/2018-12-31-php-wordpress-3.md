---
layout: post
title: "PHP Wordpress 3: Quick"
categories: web
tags: [php, website building, mysql, wordpress]
toc: 1
date: 2019-02-20
---

I use this note for all I've learned when I build again website math2it.com using Wordpress. Different from [Note of Wordpress 1](/php-wordpress-1) and [Note of Wordpress 2](/php-wordpress-2), in this note, I quickly note what I have used without clarify.

**Install offline plugins to localhost.** ([cf](http://underrootx.com/how-to-install-plugins-on-localhost-in-wordpress-without-ftp/)) : Add following line to **wp-config.php**

~~~ php
define('FS_METHOD', 'direct');
~~~

---

**Category template**: in that order: category-slug.php → category-id.php → category.php → archive.php → index.php

---

- Default page template: **page.php** file. 
- We can choose the template in the page editor.
- If page's slug is `gioi-thieu`, we can create a template for that page only, the file is **page-gioi-thieu.php**.

---

Remove `p` tag from category description: Add below line to **functions.php**

~~~ php
remove_filter('term_description','wpautop');
~~~

---

## Semantic element HTML5

- Webflow’s HTML5 tags include:

  - `<header>` defines a header for the document or a section
  - `<footer>` defines a footer for the document or a section
  - `<nav>` defines navigation links in the document
  - `<main>` defines the main content of a document
  - `<section>` defines a section in the document—the spec defines this as “a thematic grouping of content, typically with a heading," so you can think of it as being like a chapter
  - `<article>` defines an article in the document
  - `<aside>` defines content aside from the page content
  - `<address>` defines the contact information for the author/owner of a document or an article
  - `<figure>` defines self-contained content, like illustrations, diagrams, photos, code blocks, etc.
 - `<article>`: contains title and blog's content.
 - `<main>`: contains unique content of that web page (not duplicate across multiple pages). It can be only used once on each html file.

---

Automatically convert scss to css file. Using [gulp](https://gulpjs.com/)

~~~
npm install gulp-cli -g
npm install gulp -D
npx -p touch nodetouch gulpfile.js
gulp --help
~~~

and then use

~~~
sass --watch <scss folder>:<css folder>
~~~

Just use app/sass is location of scss files and public/stylesheets location where you want to have css. It will automatically convert scss to css after each save of the sass files.

## Gutengerg editor

- You may have noticed, reading [the Gutenberg documentation](https://wordpress.org/gutenberg/handbook/designers-developers/developers/tutorials/block-tutorial/writing-your-first-block-type/), that there are two ways to add new blocks. There’s ES5 and ESNext. 
- Add custom button to gutenberg block (official): [here](https://github.com/WordPress/gutenberg/tree/master/docs/designers-developers/developers/tutorials/format-api). Icon is chosen from [here](https://developer.wordpress.org/resource/dashicons/#editor-code).