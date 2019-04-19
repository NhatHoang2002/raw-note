---
layout: post
title: Gatsby 1
categories: web
toc: 1
tags: [gatsby, github, website building]
date: 2019-04-16
---

This note contains all my remarks for using [GatsbyJS](https://www.gatsbyjs.org). I wanna find a better solution for jekyll websites. I come to this framework because of [this comparison post](https://www.gatsbyjs.org/features/).

{% include toc.html %}

## Docs

- [Official documentation!](https://www.gatsbyjs.org/docs/)

## Articles

- [Why Gatsby JS is awesome and how to build and deploy a site in 10 minutes](http://www.deadcoderising.com/why-gatsby-js-is-awesome-and-how-to-build-and-deploy-a-site-in-10-minutes/): talk about features of Gatsby and a quick short tutorial to build a new website with it.
- [Why I built this blog with Gatsby.js and Contentful](https://www.halfelectronic.com/post/why-i-built-this-blog-with-gatsby-and-contentful/): a full story of a guy who is looking for a place to build his own website and why Gatsby was born. This article is really fun and attractive.
- [Building a PDF Library with Gatsby.js](http://blog.blakesimpson.co.uk/read/96-building-a-pdf-library-with-gatsby-js)

## Installation

- [npm](https://www.npmjs.com/) is the package manager for JavaScript and the world’s largest software registry
  - Install [NodeJS (with npm)](https://nodejs.org/en/) (check [this](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04) for other methods)
		~~~ bash
		sudo apt-get update
		sudo apt-get install nodejs
		~~~
  - Check the current version: `npm -v` (for npm) and `node -v` (for nodejs)
- Check version for gatsby: `gatsby -v`
- Install: `npm install --global gatsby-cli`
- If error `EACCES` occurs,
  - Create a new folder by: `mkdir ~/.npm-global`
  - Open `~/.profile`
  - Add following lines to this file
		~~~ bash
		npm config set prefix '~/.npm-global'
		export PATH=~/.npm-global/bin:$PATH
		~~~
  - Save the file and then run (if you don't restart the computer, do the same below work for new tab of terminal): `source ~/.profile`.
- Install new site
	~~~ bash
	gatsby new gatsby-site
	~~~
- Or using a [Gatsby Bootstrap Starter](https://github.com/jaxx2104/gatsby-starter-bootstrap), follow the way to install on this repo.
- Run the site: `gatsby develop` and then browse `http//localhost:8000`

## Blocks in use

- [[ref](https://www.gatsbyjs.org/tutorial/part-one/)] Any React component defined in src/pages/*.js will automatically become a page. Let’s see this in action
- **Sublime text**: install package [Babel](https://github.com/babel/babel-sublime) for the syntax highlight!
- 