---
date: 2017-03-21
title: Internet tips
description: 
categories:
  - it-tips
type: Document
use_math: false
---

## How to transfer domain from Register.com to Godaddy?

Register has a very bad service (for me) with an urgly web interface. This is the reason why I decide to change to use GoDaddy instead. After searching a little bit on the internet, it\’s not so difficult to change from Register.com to Godaddy or any other registrars. The instruction below is followed by [GoDaddy itself](http://note.dinhanhthi.com/%22https://fr.godaddy.com/help/transfer-domain-names-to-godaddy-1592/%22) and a little bit based on the guid showed on [NameCheap\’s site](http://note.dinhanhthi.com/%22https://www.namecheap.com/support/knowledgebase/article.aspx/883/83/how-to-transfer-a-domain-from-registercom/%22).

1. Unlock domain on Register.com
   - Login to [Register account](http://note.dinhanhthi.com/%22https://www.register.com/myaccount/atlas.rcmx/%22).
   - Choose Domain > Manage > Manage again beside the domain you wanna change.
   - Locate Enable/Disable Domain Lock section and click Disable Domain Lock button.
   - Choose Continue
2. Obtain Auth/EPP code
   - Also on domain manage site, locate Obtain Auth Info Code and click on it.
   - Click Continue Transfer
   - Choose Request Auth Code.
   - You should recive an email with Auth Code winthin 3-4 days.
3. Verify Contact Information
   - On My Account > Contact Information
   - It takes 24h for the changes to take effect.
4. Go to [Purchase a domain name transfer](http://note.dinhanhthi.com/%22http://www.godaddy.com/domains/domain-transfer.aspx/%22) on Godday site and type your domain (notice that, if the extension you wanna transfer isn\’t listed, you can\’t transfer to their service)
5. Finally, it\’s better to following the instruction on their own websites.


## How to use a subdomain for a wordpress site?

I meet this situation. I have a domain named **dinhanhthi.net** from **bluehost**. This wordpress site (you are reading it) is also built on bluehost server. That\’s the reason why, when I created this site for the first time, bluehost give me a choice to choose dinhanhthi.net as a domain for this site.

However, I have a main domain named **dinhanhthi.com**, this is from **godaddy**. Finally, I want to use only one domain dinhanhthi.com and this site under a subdomain **note.dinhanhthi.com**. How can I do that?

Another question, you have a wordpress, **how to assign it to a new domain**?

### Steps to do

1. **Pointing a domain to bluehost\’s nameserver** (see below). This step will help you point note.dinhanhthi.com to server of your website (bluehost) and give bluehost a right to use your domain.
2. **Change Site URL and Home URL in bluehost** (see below). This step make your site recognizes your domain that you have assigned in the previous step. Note that, I advise you to choose the same one for both site url and home url. Unless, there are some errors on loading icon on your site url.

### Change Site URL and Home URL in bluehost

Site URL is the address that visitors will see your site when they hit on the address bar. The Home URL is the address for the core files of your WordPress sites. There are 2 ways to do that, one is in **WordPress tools**, one is in **cPanel** with PhpAdmin.

Notice that, site url and home url can be different.

For **WordPress tools **(cf. [here](http://note.dinhanhthi.com/%22https://my.bluehost.com/cgi/help/wordpress-tools-urls/%22))

1. Login to [cgi panel](http://note.dinhanhthi.com/%22https://my.bluehost.com/cgi/home/%22) on bluehost.
2. On the top, choose tab **WordPress tools**
3. Choose the site you wanna change and then click **Settings** on the left side bar

For **cPanel **(cf. [here](http://note.dinhanhthi.com/%22https://my.bluehost.com/cgi/help/wordpressurl/%22))

1. Login to [cgi panel](http://note.dinhanhthi.com/%22https://my.bluehost.com/cgi/home/%22) on bluehost.
2. On the top, under Hosting and next to home, it\’s cpanel, click on it.
3. Find and choose **PhpMyAdmin**.
4. From the list of database on the left side bar, click on the database that contains your site and then choose **wp_options** or something like that. Note that, there maybe are more than one databse on your hosting.
5. On the right side panel, you will see two fields Site URL and Home URL. Click on edit and finish the rest.

### Pointing a domain to bluehost\’s nameserver

**What is a nameserver? **Nameservers for a domain name are specialized servers that translate the domain name into an IP Address that is understood by computers on the internet. Each domain name registration includes a listing of nameservers that can answer for that domain name. (this information is from bluehost help site)

1. Go to assign domain in [cgi/domains](http://note.dinhanhthi.com/%22https://my.bluehost.com/cgi/hosting/assign/%22) (need to sign in).
2. Choose \”**Use a domain that is not already associated with your account**.\” (because this domain is not created on bluehost service). In this case, I type **note.dinhanhthi.com**)
3. After filling a domain into the field, step 2 will list 2 possible nameserver to bluehost as below
4. Default for low-plan, you only have an option to choose is parked domain.
5. Click on **assign this domain**.
6. On the domain manager of your domain (in this case, I configure my domain on godaddy with the main dinhanhthi.com), choose **DNS settings**
7. Add 2 fileds > **Type** \”nameserver\” > **Name** \”note\” (note.dinhanhthi.com) > **Value** \”ns1.bluehost.com\” (162.159.24.80) and \”ns2.bluehost.com\” (162.159.25.175)

### Create a subdomain for your wordpress site on bluehost

Now, you wanna assign your wordpress site (currently is **dinhanhthi.net/note**) with a subdomain (also on bluehost\’s service, for example, note.dinhanhthi.net). You can do as (cf. [here](http://note.dinhanhthi.com/%22https://my.bluehost.com/cgi/help/274/%22))

1. Login to [cgi panel](http://note.dinhanhthi.com/%22https://my.bluehost.com/cgi/home/%22) on bluehost.
2. Choose tab **domains** > **subdomains**.
3. Enter the desired subdomain
4. Choose one of your domain names from the drop-down list
5. Enter the document root (where your site located, you can use fpt login with WinSCP on Windows or Transmit on Mac in order to log in to your bluehost accout and see in html_public that where is your wordpress site is located and with what name)
6. Click **Create**

