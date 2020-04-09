---
id: 232
title: SVN Commands
date: 2017-05-23T21:21:44+00:00
author: vish
layout: post
guid: https://blog.vishdaily.com/?p=232
permalink: /index.php/computers/subversions/svn-commands/
post_icon:
  - subversion.png
categories:
  - Subversions
tags:
  - svn
---
## 

Here are some frequently used svn commands which i regularly use for quick reference.

```bash
svn co svn://localhost/svnrepos --username vish
```

```bash
# mark missing files as delete 
svn status | grep ^! | awk '{print " --force "$2}' | xargs svn rm

# add all files
svn add * --force

```

Some admin commands

```bash
# change svn log of a perticualar commit 
svn propset --revprop -r 26 svn:log "Document nap."

# change author of a perticualar svn commit 
svn propset --revprop -r 26 svn:author "vish"

svnadmin create /svnrepos
 
# add user information 
vim /svnrepos/conf/
```