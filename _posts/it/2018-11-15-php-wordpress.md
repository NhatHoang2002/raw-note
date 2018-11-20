---
title: PhP Wordpress
categories: web
tags: [php, website building, mysql]
toc: 1
---

I use this note for all I've learned when I build again website math2it.com using Wordpress.

## Install LAMP on Linux

0. I followed [Tania's post](https://www.taniarascia.com/local-environment/) for setting up a local enviroment. She used MAMP (on Mac) while I use Linux.
1. [Download LAMP](https://bitnami.com/stack/lamp/installer) on bitnami and install it (double click on file **.run** and follow the instructions)
2. **phpMyAdmin**: after installing successfully LAMP, one can access phpMyAdmin at _http://127.0.0.1:8080/phpmyadmin_ with username **root** and password like the one you gave when installing LAMP.
3. Open **Bitnami LAMP Stack** > **Apache Web Server** > **Configure** > **Open Conf file** > change the line

	~~~
# ServerRoot "/home/thi/lampstack-7.1.24-0/apache2"
# to
ServerRoot "/home/thi/Documents/learnwordpress"
	~~~

4. And then click on **Restart** the _Apache Web Server_.