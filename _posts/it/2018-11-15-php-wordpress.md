---
title: PhP Wordpress 1
categories: web
tags: [php, website building, mysql]
toc: 1
date: 2018-11-20
---

I use this note for all I've learned when I build again website math2it.com using Wordpress.

## Install LAMP on Linux

### Install Apache2 and Mysql server

Follow [this article](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-ubuntu-18-04) on digitalocean to install LAMP on Linux. Below are all neccessary command lines.

~~~ bash
# upate system
sudo apt update

# install apache2
sudo apt install apache2

# Adjust the Firewall to Allow Web Traffic
sudo ufw app list
sudo ufw app info "Apache Full" # it should show that it enables traffic to ports 80 and 443
sudo ufw allow in "Apache Full"
# try browsing http://localhost

# install mysql
sudo apt install mysql-server

# setup mysql (choose Y for all, set passwords if neccessary)
sudo mysql_secure_installation
sudo mysql
SELECT user,authentication_string,plugin,host FROM mysql.user;
# change 'YourPassword' with your own password!!!
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'YourPassword';
FLUSH PRIVILEGES;
# verify that 'root' has 'mysql_native_password' in filed 'plugin'
SELECT user,authentication_string,plugin,host FROM mysql.user;
exit
~~~

After set a new password to **root** user of mysql, instead of using `sudo mysql`, you have to use following command to access mysql with the root

~~~ bash
mysql -u root -p # and then type the new password (YourPassword above)!
~~~

### Install PHP

Following the same article as above,

~~~ bash
# install php
sudo apt install php libapache2-mod-php php-mysql

# tell web server to prefer .php file
sudo gedit /etc/apache2/mods-enabled/dir.conf
# find IfModule mod_dir.c and move index.php to the first
# restart apache webserver
sudo systemctl restart apache2

# check status on apache2
sudo systemctl status apache2 # press Q to exit

# install some additional modules
apt search php- | less # press Q to quit
~~~

Testing a php file in **/var/www/html/**

~~~ bash
sudo gedit /var/www/html/info.php
~~~

and paste 

~~~ php
<?php
phpinfo();
?>
~~~

Goto **[localhost/info.php](http://localhost/phpmyadmin)** to test

## Install phpMyAdmin

I followed [this article](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-18-04) on DigitalOcean. Below are all command lines

~~~ bash
# install phpmyadmin
sudo apt update
sudo apt install phpmyadmin php-mbstring php-gettext
# choose apache2 as default if you are asked for this

# enable the mbstring PHP extension
sudo phpenmod mbstring

# restart Apache for your changes to be recognized
sudo systemctl restart apache2
~~~

- If you meet error **ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO)**, follow [this help](https://stackoverflow.com/a/48748685/1323473) on stackoverflow.
- If you have error **Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock'**, check [this](https://stackoverflow.com/questions/11990708/error-cant-connect-to-local-mysql-server-through-socket-var-run-mysqld-mysq).
- If **Job for mysql.service failed because the control process exited with error code.**

**ALL ABOVE ERRORS**: Try to remove and reinstall again mysql and 

~~~ bash
sudo apt-get remove --purge mysql*
sudo apt-get autoremove
sudo apt-get autoclean
sudo apt-get install mysql-server mysql-client
~~~

### Working in Mysql

Login to mysql

~~~ bash
mysql -u root -p
~~~

See the list of current user in mysql

~~~ bash
# in the mysql environment
SELECT user,authentication_string,plugin,host FROM mysql.user;
~~~

Create a new user and give it a strong password

~~~ bash
CREATE USER 'thi'@'localhost' IDENTIFIED BY 'YourPassword';
~~~

Grant your new user appropriate privileges

~~~ bash
GRANT ALL PRIVILEGES ON *.* TO 'thi'@'localhost' WITH GRANT OPTION;
~~~

After installing phpmyadmin, there has to be an user `phpmyadmin` in the list of user of mysql, if not, you need to create a such user and give it grant control like above.

### Go to phpMyAdmin

- Go to **[http://localhost/phpmyadmin](http://localhost/phpmyadmin)**
- Login with your user and password you created above (`thi` for example).

## Change apache2 root document

- The Apache server is installed on **/var/www/html**.
- Simply download [this tool](https://github.com/hsb4995/Apachange) and follow the instructions. You can also check the author's [answer](https://askubuntu.com/a/738527/248456) on SE.

## Install and setup wordpress

I mainly followed these steps but sometimes (for example, install wodpress on localhost, I did myself!)

- [Download WP](https://wordpress.org/download/)
- Extract the zip file to the root folder of apache2.
- Open **http://localhost/phpmyadmin**, log in with the user you created before (e.g. _thi_), create a database whose name is **wordpress**. Notethat, you need to remember and be sure that the database's name + user + password are the same with the one in next steps.
- Open **http://localhost**, you will see a installation site.
- Follow the steps in this site, remember to fill in the infor I noted above.
- After installing successfully WP, you meet the login page, fill out your username and password to log it in.
- Cf. [WP official documentation](https://codex.wordpress.org/) and [StackOverflow-WP](https://stackoverflow.com/questions/tagged/wordpress)

### WP theme

- The themes will be stored in **./wp-content/themes**.
- Create a new folder for your theme, I call it **math2itwp**
- **Note that**: A WordPress theme needs only two files to exist – **style.css** and **index.php**.
- You can download [this example theme](https://github.com/taniarascia/bootstrapblog) (bootstrap 3 starter theme), extract the zip file which contains 2 files **index.html** and **blog.css**. Rename index.html to index.php and then copy these 2 files to **themes** folder. 
- Back to wordpress manage page (**http://localhost/wp-admin/**). Choose **math2itwp** as a main theme and then reload the page and see the changes.
- Note that, **blog.css** is not loaded yet, <mark>learn right now that you can never link to anything in a WordPress page without some PHP.</mark>
  - Change in **index.php** the line

    ~~~ php
    <!-- old code -->
    <link href="blog.css" rel="stylesheet">

    <!-- new one -->
    <link href="<?php echo get_bloginfo('template_directory'); ?>/blog.css" rel="stylesheet">
    ~~~

### Split into parts

We now wanna split the unique **index.php** into parts like _header.php, footer.php, sidebar.php,..._

- Before `</head>` in **header.php**, add `<?php wp_head();?>`
- Before `</body>` in **footer.php**, add `<?php wp_footer();?> `
- Just cut and copy lines relating to header, footer, content and sidebar to the corresponding php files.
- In the **index.php**,

  ~~~ php
  <!-- header -->
  <?php get_header(); ?>

  <!-- content -->
  <?php get_template_part( 'content', get_post_format() ); ?>

  <!-- sidebar -->
  <?php get_sidebar(); ?>

  <!-- footer -->
  <?php get_footer(); ?>
  ~~~navigation

## Wordpress' components

### Site's components

Normally, we use

~~~ php
<?php echo <!-- commands -->; ?>
~~~

- Website's name: `get_bloginfo( 'name' )`
- Website's description: `get_bloginfo( 'description' )`
- Homepage's url: `get_bloginfo( 'wpurl' )`
- Template's directory: `get_bloginfo('template_directory')`

### Loops

~~~ php
<?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>
<!-- contents of the loop -->
<?php endwhile; endif; ?>
~~~

### Post's components

Normally, we use 

~~~ php
<?php <!-- commands -->; ?>
~~~

- Post's content: `the_content()`
- Post's title: `the_title()`
- Post's date: `the_date()`
- Post's author: `the_author()`

### Sidebar

Wordpress archives

~~~ php
<ol class="list-unstyled">
  <?php wp_get_archives( 'type=monthly' ); ?>
</ol>
~~~

### Author's components

- Description: `<?php the_author_meta( 'description' ); ?>`

### Navigation

- List of pages: `<?php wp_list_pages( '&title_li=' ); ?>`
  - `'title_li='` is telling the code not to add a “Pages” title before the list. 

### Page's layout

For pages, you can create a new **page.php** with different layout. All pages will use this layout to display the content.

## Errors

In the case you cannot use other Permalink settings than **Plain**, for example you cannot reach _localhost/post-name_ and only be able to reach the homepage. <mark>If you just need to build the theme</mark>, use **Plain** (with post id), everything goes right!

**Solution!!!!**: Create a new file called **.htaccess** in root folder (folder with folder _wordpress-content_). Put inside it with the contents provided when you click **Save** in the **Permalink Settings** of WP admin. Normally, this is

~~~
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]
</IfModule>
~~~

Try to refresh the page and see the changes!!!!