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

```bash
kdesu dolphin
```

## Change Password Of dmg files

```bash
hdiutil chpass <dmg_file_name>
```

## Secure Delete Deleted Files

**Warning!** It’s _critically important_ that you include the `freespace` portion of that command. If you don’t, `diskutil` will happily start securely erasing the entire disk, instead of just the free space!

```bash
# diskutil list
```

```bash
diskutil secureErase freespace 1 /dev/disk3s4
```

## Check how fast is your mac write data to its disk

```bash
time dd if=/dev/zero bs=1024k of=tstfile count=1024
```

## Secure Delete Files / Folders

```bash
srm <file_name> 
srm -r <folder_name>

```