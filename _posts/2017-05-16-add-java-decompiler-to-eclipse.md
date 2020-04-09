---
id: 165
title: Add Java Decompiler To Eclipse
date: 2017-05-16T10:34:38+00:00
author: vish
layout: post
guid: https://blog.vishdaily.com/?p=165
permalink: /index.php/computers/developer-tools/add-java-decompiler-to-eclipse/
post_icon:
  - eclipse.png
categories:
  - Developer Tools
tags:
  - eclipse
---
Every time i install eclipse it is a pain trying various methods to add de-compiler plugin to eclipse. This method is always working for me.

In your eclipse, Go to Help -> Install New Software -> Click on Add, Then paste the following update site url in both Name and Location fields

```bash
http://mchr3k-eclipse.appspot.com/
```

  1. Selecting the above url from the drop down, displays available plugins from the update site.
  2. From the list select &#8216;Java Decompiler Eclipse Plug-in&#8217;
  3. And Click on Next. Accept if you get any notifications meanwhile positively. Note that in the below image Next button is grayed out because for me its already installed.
  4. Restart eclipse.
  5. For testing, Open any class file now (Search using short cut Ctrl + T from libraries)
  6. You should be able to successfully see the de-compiled java code of the class file.

Note: If the de-compiled code is not displayed automatically, on the menu bar, click the small blue icon in the menu.

&nbsp;

&nbsp;

&nbsp;

&nbsp;