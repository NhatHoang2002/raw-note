---
title: Jekyll & Liquid note
categories: web
toc: 1
tags: ["jekyll", "liquid", website building]
maths: 1
date: 2018-10-20
---

{% include toc.html %}

## Liquid and Jekyll

Jekyll is written in [Liquid language](https://help.shopify.com/themes/liquid), here are some syntaxes

**Case statement**

~~~ ruby
{%raw%}{% case template %}

{% when 'label' %}
     // {{ label.title }}
{% when 'product' %}
     // {{ product.vendor | link_to_vendor }} / {{ product.title }}
{% else %}
     // {{page_title}}
{% endcase %}{%endraw%}
~~~

Write [liquid code in jekyll](http://stackoverflow.com/questions/3426182/how-to-escape-liquid-template-tags)

### Những keywords quan trọng

- `{%raw%}{{ site.url }}{%endraw%}` : địa chỉ trang web.

### Thêm code liquid trong jekyll

- Nếu muốn thêm tag `{{"{% this "}}%}` thì ghi `{% raw %}{{"{% this "}}%}{% endraw %}`.
- Còn nếu muốn thêm `{{"{{ this "}}}}` thì ghi `{% raw %}{{"{{ this "}}}}{% endraw %}`.

Quan trọng là mở đầu bằng `{% raw %}{{"{% endraw %}` trước từ khóa và kết thúc bằng `{% raw %}"}}{% endraw %}` trước kết thúc từ khóa.

Hoặc một cách khác dễ hơn, đó là dùng `{{ "{% raw " }}%}` và `{{ "{% endraw " }}%}` bao quanh từ khóa cầ nhiện. Hai từ này còn có thể dùng để hiện một đoạn code nếu được đặt trước đó.

~~~
{{ "{% raw " }}%}{% raw %}{% for %}

{% end for %}{% endraw %}{{ "{% endraw " }}%}
~~~

## Thêm tag cho dinhanhthi.com

- Thêm file trong thư mục `tag` và đổi một số nội dung trong đó.
- Thêm vài dòng cho tag đó trong file _data/tags.yml

## Bibliography in Jekyll

**VERY IMPORTANT!!!** Vì lý do bảo mật nên github pages không cho dùng mấy cái plugins bên ngoài, do đó không thể deploy theo cách thông thường với jekyll-scholar được. Có 1 cách là deploy locally rùi sau đó đưa lên github pages nhưng tạm thời chưa biết!!!!

The main instruction and plugin is [here](https://github.com/inukshuk/jekyll-scholar) and [here](https://pages.lip6.fr/Pascal.Poizat/blog/posts/2016/02/01/jekyll-and-bibtex/), we will use `jekyll-scholar`

1. You must have ruby on your computer (Windows), you can download and install it from [here](https://rubyinstaller.org/).
2. Download **DevKit** also from above site. Actually, because you will meet some error something like `The unicode native gem requires installed build tools`, follow [this step](https://stackoverflow.com/questions/8100891/the-json-native-gem-requires-installed-build-tools), I write a gain as below.
	- Extract DevKit to path C:\Ruby193\DevKit
	- Press **Start**, type "Ruby" and choose **Start Command Prompt with Ruby** and then
	- Run `cd C:\Ruby193\DevKit`
	- Run `ruby dk.rb init`
	- Run `ruby dk.rb review`
	- Run `ruby dk.rb install`
	- Try install following to confirm that DevKit successfully installed
	~~~
	gem install json --platform=ruby
	ruby -rubygems -e "require 'json'; puts JSON.load('[42]').inspect"
    ~~~
3. Insyall plugin `jekyll-scholar`
	~~~
    gem install jekyll-scholar
    ~~~
4. Add `gems: - jekyll-scholar` into `_config.yml` file.
5. Add `gem \'jekyll-scholar\'` in `Gemfile` file

There is an error when publish to github page, plugin jekyll không được nhận!!!

## Jekyll, markdown and Mathjax

If you use mathjax rendering on your jekyll sites, there maybe sometimes are errors on the rendering of maths equations. This is the list of remarks on this problem.

- $\vert \vert$ : Don't use `||` for absolute values, use `\vert{}\vert` instead. This because jekyll understand this as a table generator instead of an absolute value.
- $\Vert \Vert$ : Don't use `\left\| \right\|`, use `\Vert{}\Vert` instead.
- $g\ast$ : **Star symbol**, Don't use `*`, use `\ast` instead. Otherwise, jekyll understand this symbol as italic.
- $f\_1 g\_1$ : problem with underscore symbol. Instead of using `_` for many times, use `\_`. Vấn đề này chủ yếu xảy ra nếu ta dùng `$ $` inline, còn nếu dùng 2 dấu `$` thì sẽ không cần `\_`.

## Girhub pages + domains

### Github/Jekyll : How to add a custom domain in Github Page?

My personal websites (dinhanhthi.com) is written by Jekyll + Github Page (yes, I don’t lose any money except the domain). This is the great way to build a static website (personal website, product introduction website,…). The default domain address when you create your own website via this way is **yourname.github.io**. In this post, I will show you the very easy way to add custom domain like yourname.com pointing to your github pages.

1. In your main repository, create a file **CNAME** (without any extension) whose content is your custom domain (for example, **yourname.com**) (don’t add www or http or anything else before yourname.com). Then commit and sync.
2. In your file **_config.yml**, change the line “url” by “**url: “http://yourname.com”**“
3. Go to your domain’s manager website (I use Godaddy), step to DNS settings and then add three fields.
   1. “**A**” record for “**@**” to “**192.30.252.153**“
   2. “**A**” record for “**@**” to “**192.30.252.154**“
   3. “**CNAME**” record for “**www**” to “**yourname.github.io**“
4. Make sure that there is no conflict with the same host in your DNS settings (i.e., the same record values pointing to different targets.
5. Finish.

### How to use custom subdomain for Jekyll Github Pages?

Go to DNS settings of your domain. Add a `CNAME` from `yoursub.yourdomain.com` pointing to `yourname.github.io`.

Create a file `CNAME` in the root folder of your github page (without any extension) whose content only is `yoursub.yourdomain.com`.

Change `url` in `_config.yml` with `"http://yoursub.yourdomain.com"`

Submit and Sync.

### Make github pages automatically forward to another page

I have two github page websites, one is **site1.github.io**, the other is **site2.github.io**. Now I want site1 forward automatically to site2. How I can do that? It’s so easy with few lines of html code.

In your repository, create ONLY ONE file index.html with the content

~~~ html
<head>
<meta http-equiv="refresh" content="0; url=http://site2.github.io/" />
</head>

<html>
<head>
<title>Welcome</title>
</head>
<body>

</body>
</html>
~~~

## Local jekyll site

Only regenerate the changed file (more quickly): 

~~~ bash
bundle exec jekyll serve -I true
~~~