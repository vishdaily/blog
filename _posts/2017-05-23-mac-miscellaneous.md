---
id: 228
title: Mac Miscellaneous
date: 2017-05-23T21:20:40+00:00
author: vish
layout: post
guid: https://blog.vishdaily.com/?p=228
permalink: /index.php/computers/mac/mac-miscellaneous/
post_icon:
  - mac-finder.png
categories:
  - Mac
tags:
  - dolphin
  - mac finder
---
## Run dolphin file manager as root

Some system files are visible in mac finder only when it opened with root privileges.

<pre class="lang:sh decode:true">kdesu dolphin</pre>

## Change Password Of dmg files

<pre class="lang:sh decode:true ">hdiutil chpass &lt;dmg_file_name&gt;</pre>

## Secure Delete Deleted Files

**Warning!** It’s _critically important_ that you include the `freespace` portion of that command. If you don’t, `diskutil` will happily start securely erasing the entire disk, instead of just the free space!

<pre class="lang:sh decode:true "># diskutil list</pre>

<pre class="lang:sh decode:true">diskutil secureErase freespace 1 /dev/disk3s4</pre>

## Check how fast is your mac write data to its disk

<pre class=""><code>time dd if=/dev/zero bs=1024k of=tstfile count=1024</code></pre>

## Secure Delete Files / Folders

<pre class="lang:sh decode:true">srm &lt;file_name&gt; 
srm -r &lt;folder_name&gt;
</pre>