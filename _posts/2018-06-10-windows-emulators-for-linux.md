---
id: 556
title: Windows Emulators For Linux
date: 2018-06-10T13:58:57+00:00
author: vish
layout: post
guid: https://blog.vishdaily.com/?p=556
permalink: /index.php/computers/linux/windows-emulators-for-linux/
post_icon:
  - linux
categories:
  - Linux
tags:
  - linux
  - windows-emulators
  - wine
---
## DOSBox

Ever faced in a situation that you wanted to run Windows Applications (.exe) in Ubuntu ? Thanks to DOSBox.

<li style="list-style-type: none;">
  <ol>
    <li>
      Download DOSBox from Ubuntu Software Center
    </li>
    <li>
      Go to http://turbo-c.soft32.com and download the zip file and extract it to ~/tc
    </li>
    <li>
      Open DOSBox and type the following
    </li>
    <li>
      mount c ~/tc/TURBOC3/BIN
    </li>
    <li>
      c:
    </li>
    <li>
      TC.exe
    </li>
  </ol>
</li>

Some Short Cuts

<li style="list-style-type: none;">
  <ol>
    <li>
      Ctrl + F10 For releasing mouse from the DOSBox window.
    </li>
    <li>
      Alt + Enter For Full Screen
    </li>
    <li>
      Edit dosbox-{version}.conf<br /> For Linux the configfile is created on the first run in ~/.dosbox/ The name is dosbox-&lt;i>{version}&lt;/i>.conf where version is currently 0.74
    </li>
  </ol>
</li>

```bash
fullscreen=true
fulldouble=true
fullresolution=1366x768
windowresolution=1366x768
&lt;strong>output=opengl&lt;/strong>
autolock=true
```

There are other alternatives if you want to run TurboC on Linux [codeblocks](http://codeblocks.org/) and NetBeans

## Wine (Wine Is Not an Emulator)

According to https://www.winehq.org Wine is a compatibility layer capable of running Windows applications on several POSIX-compliant operating systems, such as Linux, macOS, & BSD.

&nbsp;