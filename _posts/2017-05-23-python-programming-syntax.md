---
id: 262
title: Python Programming Syntax
date: 2017-05-23T13:31:30+00:00
author: vish
layout: post
guid: https://blog.vishdaily.com/?p=262
permalink: /index.php/computers/programming-languages/python-programming-syntax/
post_icon:
  - python.png
categories:
  - Programming Languages
tags:
  - python
---
A quick reference for python installation, syntax and etc.

# Installation

```bash
apt-get install python3
apt-get install python3-pip python3-wheel
```

# Syntax

## if

```bash
if expression:
        print "True"
    elif expression:
        print "False"
     else:  
        print "False"

```

## multi line

<pre>total = item_one + \ 
        item_two + \
        item_three
 
days = ['Monday', 'Tuesday', 'Wednesday',
         'Thursday', 'Friday']
```

Statements contained within the [], {}, or () brackets do not need to use the line continuation character.

## print

<pre>print ( 'Key is : {}  -  {}'.format(key, servername ))
```

## while

<pre>def ask_ok(prompt, retries=4, reminder='Please try again!'):     
    while True:         
        ok = input(prompt)         
        if ok in ('y', 'ye', 'yes'):             
            return True         
        if ok in ('n', 'no', 'nop', 'nope'):             
            return False         
        retries = retries - 1         
        if retries < 0:             
            raise ValueError('invalid user response')         
        print(reminder)

```

## dictionary declaration

<pre>ansible_groups                 =        dict()
    if key in ansible_groups:
        ansible_groups[key].append(servername)
    else:
        ansible_groups[key]        =        [servername]

```

## looping

<pre>for key, value in sorted(ansible_groups.items()):
        print (key)
        for servername in value:
            print ( "---", servername )
        print ("")

    for index, value in enumerate(groupsplit):
        print (index)

```

## string functions

<pre>split
        group_split = key.split('|')
    lower
        str.lower()
        str.rsplit("_",3)

    "1_2_3_4_5".rsplit("_",1) ==> ['1_2_3_4', '5']
    "1_2_3_4_5".rsplit("_",2) ==> ['1_2_3, '4', '5']
    "1_2_3_4_5".rsplit("_",3) ==> ['1_2, '3', '4', '5']


```