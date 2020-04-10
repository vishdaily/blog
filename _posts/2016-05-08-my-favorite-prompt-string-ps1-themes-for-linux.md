---
id: 13
title: My Favorite Prompt String (PS1) And Colorizing echo
date: 2016-05-08T16:09:44+00:00
author: vish
layout: post
guid: https://blog.vishdaily.com/?p=13
permalink: /index.php/computers/linux/my-favorite-prompt-string-ps1-themes-for-linux/
post_icon:
  - linux.png
categories:
  - linux
tags:
  - shell
  - terminal
---
Following are my favorite PS1 strings which i use frequently in my bashrc file.

```bash

PS1="\n\[\033[38;5;10m\]$(printf %*s $COLUMNS | tr ' ' '-')\n\[\033[38;5;207m\]\d\[\]\[\033[38;5;15m\] \[\]\[\033[38;5;51m\]\t\[\]\[\033[38;5;15m\] \[\]\[\033[38;5;11m\]\u\[\]\[\033[38;5;15m\]@\[\]\[\033[38;5;206m\]\H\[\]\[\033[38;5;201m\]: \[\]\[\033[38;5;47m\]\w\[\]\[\033[38;5;15m\]\n\[\]\[\033[38;5;207m\]$\[\]\[\033[38;5;15m\] \[\]"

PS1="\n\[\033[38;5;207m\]\d \T \[\033[38;5;10m\]\u @ \[\033[38;5;51m\]\H : \[\033[38;5;15m\]\w\n\[\033[38;5;207m\]\[\033[38;5;15m\]$ "


```

This looks like this 🙂

<img class="alignnone wp-image-168 size-full" src="https://blog.vishdaily.com/wp-content/uploads/2016/05/2017-05-16_16h55_18.png" alt="" width="957" height="203" srcset="https://blog.vishdaily.com/wp-content/uploads/2016/05/2017-05-16_16h55_18.png 957w, https://blog.vishdaily.com/wp-content/uploads/2016/05/2017-05-16_16h55_18-300x64.png 300w, https://blog.vishdaily.com/wp-content/uploads/2016/05/2017-05-16_16h55_18-768x163.png 768w, https://blog.vishdaily.com/wp-content/uploads/2016/05/2017-05-16_16h55_18-150x32.png 150w" sizes="(max-width: 957px) 100vw, 957px" /> 

You can customize one for your self in this useful site <http://bashrcgenerator.com/>

But this is one liner to get all the colors codes int your command prompt and decide your self.

```bash
printf "\nForeground %s\nBackground %s\n\n" "\033[38;5;COLOR_CODE" "\033[48;5;COLOR_CODE"; for i in {0..256}; do echo -en "\033[38;5;${i}m${i}m "; done; printf "\n";
```

<img class="alignnone wp-image-598 size-full" src="https://blog.vishdaily.com/wp-content/uploads/2016/05/2018-09-14_11h59_50.png" alt="" width="1381" height="200" srcset="https://blog.vishdaily.com/wp-content/uploads/2016/05/2018-09-14_11h59_50.png 1381w, https://blog.vishdaily.com/wp-content/uploads/2016/05/2018-09-14_11h59_50-300x43.png 300w, https://blog.vishdaily.com/wp-content/uploads/2016/05/2018-09-14_11h59_50-768x111.png 768w, https://blog.vishdaily.com/wp-content/uploads/2016/05/2018-09-14_11h59_50-1024x148.png 1024w, https://blog.vishdaily.com/wp-content/uploads/2016/05/2018-09-14_11h59_50-150x22.png 150w" sizes="(max-width: 1381px) 100vw, 1381px" /> 

**Colorize echo in Bash**

Bash uses numeric codes to set attributes of the text to be displayed.

<u>Attribute codes:</u>  
00=none 01=bold 04=underscore 05=blink 07=reverse 08=concealed

<u>Text color codes:</u>  
30=black 31=red 32=green 33=yellow 34=blue 35=magenta 36=cyan 37=white

<u>Background color codes:</u>  
40=black 41=red 42=green 43=yellow 44=blue 45=magenta 46=cyan 47=white
