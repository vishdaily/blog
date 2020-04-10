---
id: 11
title: Few Developer Friendly Tools For Windows
date: 2016-05-08T13:07:20+00:00
author: vish
layout: post
guid: https://blog.vishdaily.com/?p=11
permalink: /index.php/computers/developer-tools/few-developer-friendly-tools-for-windows/
post_icon:
  - windows.png
categories:
  - developer-tools
tags:
  - developer-tools
  - windows
---
I want to share you all about some of my favorite tools / software&#8217;s I use which assist me in my daily development tasks.

**CygWin,** an opensource project brings linux shell environment to Windows. However, future windows 8 will also bring linux shell as inbuilt in to Window but do not know yet what features will it bring in.

 <span style="color: #3366ff;"><a style="color: #3366ff;" href="https://www.cygwin.com/">https://www.cygwin.com/</a></span>

**Deskpins,** is simple cool freeware application to make a specific window always on top. I use it every day.

 <span style="color: #3366ff;"><a style="color: #3366ff;" href="http://deskpins.en.softonic.com/">http://deskpins.en.softonic.com/</a></span>

**Ditto,** is an opensource clipboard manager tool always comes handy when you need it. Cool thing is it allows you to save any type of info (text, media etc) and able to access it.

 <span style="color: #3366ff;"><a style="color: #3366ff;" href="http://ditto-cp.sourceforge.net/">http://ditto-cp.sourceforge.net/</a></span>

**Stickies,** is a free stickies application. It is very simple and has many features which are very helpful and interesting.

<span style="color: #3366ff;"><a style="color: #3366ff;" href="http://www.zhornsoftware.co.uk/"> http://www.zhornsoftware.co.uk/</a></span>

**CSVed,** is an advanced csv editor. It has various functions that you can perform on a csv file. Comes very handy.

 <span style="color: #3366ff;"><a style="color: #3366ff;" href="http://csved.sjfrancke.nl/">http://csved.sjfrancke.nl/</a></span>

**CSVFileView,** yet another CSV file viewer. Its very light weight clean and simple.

 <span style="color: #3366ff;"><a style="color: #3366ff;" href="http://www.nirsoft.net/utils/csv_file_view.html">http://www.nirsoft.net/utils/csv_file_view.html</a></span>

**Notepad++,** Opensource text editor for windows. I wish they also release it for Mac.

 <span style="color: #3366ff;"><a style="color: #3366ff;" href="https://notepad-plus-plus.org/">https://notepad-plus-plus.org/</a></span>

**Nulloy,** is a free music player with a wave form. It displays the sound clip in terms of a wave form so you know exactly at which time the sound starts. I looked at all the music players or video applications for such a feature i could only find it here. Please let me know if you know any other tool better than this.

 <span style="color: #3366ff;"><a style="color: #3366ff;" href="http://nulloy.com/">http://nulloy.com/</a></span>

**Putty,** free ssh client to connect to linux servers.

 <span style="color: #3366ff;"><a style="color: #3366ff;" href="http://www.putty.org/">http://www.putty.org/</a></span>

**SuperPutty,** just an addon to putty which supports multiple tabs. It reads the configuration from Putty.

 <span style="color: #3366ff;"><a style="color: #3366ff;" href="https://github.com/jimradford/superputty/releases">https://github.com/jimradford/superputty/releases</a></span>

**TCPView,** is a tool from sysinternals, allows you to see detailed listings of all TCP and UDP endpoints on your system, including the local and remote addresses and state of TCP connections.

 <span style="color: #3366ff;"><a style="color: #3366ff;" href="https://technet.microsoft.com/en-us/sysinternals/tcpview.aspx">https://technet.microsoft.com/en-us/sysinternals/tcpview.aspx</a></span>

**SoapUI,** is a free Testing tool to automate or test webservices.

 <span style="color: #3366ff;"><a style="color: #3366ff;" href="https://www.soapui.org/">https://www.soapui.org/</a></span>

**Pidgin,** is a free chat client. It supports many chat networks.

 <span style="color: #3366ff;"><a style="color: #3366ff;" href="https://www.pidgin.im/">https://www.pidgin.im/</a></span>

**ConEmu** for windows. This has been my favorite replacement for windows command prompt from almost 3 years and made my developer life easier. With this i could configure my startup directory paths and initial batch files to be executed every time i open ConEmu. My requirement was that, the kind of projects I was working required at least 5 or 6 command to be opened and then some batch files to be executed which sets few environment variables. One window takes care of application server, Another displays &#8220;tail -f error.log&#8221; application server log (I have also installed **cygwin** to be able to execute linux commands) and so on.. It also allows to define tasks for different projects. Each task consists of one or more batch commands. for example

```bash
> "%windir%\system32\cmd.exe" /k "cd C:\dev\programs\eserver72136\bin"

* "%windir%\system32\cmd.exe" /k "C:\dev\programs\eserver72136\bin\environment.bat && cd C:\dev\programs\eserver72136\bin"

* "%windir%\system32\cmd.exe" /K "C:\dev\programs\eserver72136\bin\environment.bat && cd C:/dev/projects/haefele/sources/eclipsesvn/current/eserver/source/build"

* "%windir%\system32\cmd.exe" /K "C:\dev\programs\eserver72136\bin\environment.bat && cd C:/dev/projects/haefele/sources/eclipsesvn/previous/eserver/source/build"

* "%windir%\system32\cmd.exe" /K "C:\dev\programs\eserver72136\bin\environment.bat && cd C:/dev/projects/haefele/sources/eclipsesvn/current/eserver/source/haefele_dbinit_template/build"

* powershell.exe -new_console:a -noexit -command "cd C:\dev\projects\haefele\sources\eclipsesvn\current\eserver\source"
```

<span style="color: #3366ff;"><a style="color: #3366ff;" href="https://conemu.github.io/">https://conemu.github.io/</a></span>

&nbsp;