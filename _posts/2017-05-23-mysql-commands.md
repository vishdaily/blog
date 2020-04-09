---
id: 240
title: Mysql Commands
date: 2017-05-23T21:21:57+00:00
author: vish
layout: post
guid: https://blog.vishdaily.com/?p=240
permalink: /index.php/computers/databases/mysql-commands/
post_icon:
  - mysql.png
categories:
  - Databases
tags:
  - mysql
---
&nbsp;

Here are some frequently used mysql commands for quick reference.

<pre class="lang:mysql decode:true ">mysql -u root -p &lt;enter&gt;
mysql -u root -p'yourpassword'</pre>

<pre class="lang:mysql decode:true ">CREATE USER 'user'@'localhost' IDENTIFIED BY 'your_password';
CREATE database INVERNTORY;
GRANT ALL PRIVILEGES ON inventory.* TO 'community'@'localhost' IDENTIFIED BY 'password' WITH GRANT OPTION;
</pre>

<pre class="lang:mysql decode:true "># import database 
mysql -u username -p password [databasename] &lt; [sql file name]
# export database 
mysqldump -u username -p'password' [databasename] &gt; [sql file name] 
# copy or clone a database
mysqldump -u &lt;user name&gt; -p'yourpassword' &lt;original_db&gt; | mysql -u &lt;user name&gt; -p'yourpassword' &lt;new db&gt;
</pre>

&nbsp;