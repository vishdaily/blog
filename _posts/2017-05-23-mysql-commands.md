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

```bash
mysql -u root -p <enter>
mysql -u root -p'yourpassword'
```

```bash
CREATE USER 'user'@'localhost' IDENTIFIED BY 'your_password';
CREATE database INVERNTORY;
GRANT ALL PRIVILEGES ON inventory.* TO 'community'@'localhost' IDENTIFIED BY 'password' WITH GRANT OPTION;

```

```bash
# import database 
mysql -u username -p password [databasename] < [sql file name]
# export database 
mysqldump -u username -p'password' [databasename] > [sql file name] 
# copy or clone a database
mysqldump -u <user name> -p'yourpassword' <original_db> | mysql -u <user name> -p'yourpassword' <new db>

```

&nbsp;