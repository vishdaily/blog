---
id: 201
title: 'Package Managers For Mac &#8211; Homebrew &#038; MacPorts'
date: 2017-05-21T15:48:09+00:00
author: vish
layout: post
guid: https://blog.vishdaily.com/?p=201
permalink: /index.php/computers/mac/package-managers-for-mac-homebrew-macports/
post_icon:
  - mac-osx.png
categories:
  - Mac
tags:
  - homebrew
  - mac
---
Like apt-get for Debian, yum for Red Hat Linux Operating Systems, there are couple of package manager for Mac. **Homebrew,** **MacPorts** and **Fink** The packages are build / developed on Darwin OS which is base for mac. This enables the packages to work also on mac.

# So which one to choose ?

Personally, i have both Homebrew and MacPorts. I haven&#8217;t find any need to install Fink. But you can choose which one you can go with. The basic difference between brew and port i see is that, **brew** leverages most of the functionality from OSX so less time and space to setup. You don&#8217;t want to care about much and just want the stuff to work. All of its packages are depending mostly on existing Mac version **port **has a largest selection of packages to install. It will build every package on its own and doesn&#8217;t depend on OSx base. I would go with port unless i don&#8217;t find any specific package with it. **Fink **on the other hand is inspired by debians apt-get style and has precompiled packages. I haven&#8217;t tried it though.

# Homebrew

Package manager for Mac.

https://brew.sh

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## Some frequently used commands

```bash
brew search &lt;package&gt;
brew info &lt;imagemagick&gt;
brew install &lt;package&gt;
brew --dry-run uninstall &lt;package&gt;
brew reinstall &lt;imagemagick&gt;
brew list # displays list of installed packages
brew leaves # displays formulas that are not dependent on other installed formulas
```

```bash
# Remove all the packages installed by brew
brew list -1 | xargs brew rm

# unlink the tool short cut and link again if the command is not found after installation
brew unlink imagemagick && brew link imagemagick 

# Displays brew local path
brew --prefix 

# uninstall the dependencies of the package you installed
brew deps terminator | egrep -v "openssl|gettext" | xargs brew uninstall

# List dependencies of the given formula 
brew deps osxfuse

```

# MacPorts

Another package manager for Mac.

https://www.macports.org

## Some frequently used commands

```bash
sudo port search &lt;portname&gt;
sudo port info &lt;portname&gt;
sudo port install &lt;portname&gt;

# Lists the ports installed with out dependencies. (which are not depended on other installed ports)
sudo port echo leaves

# List the installed ports including the dependencies
sudo port installed
port -d echo installed 
du -sh /opt/local/var/macports/software/* 

sudo port uninstall &lt;portname&gt; 
sudo port uninstall --follow-dependencies &lt;portname&gt; 

# Before pruning your leaves, you may also want to uninstall old versions of ports that are no longer “active”
sudo port uninstall inactive

# displays dependencies of the port
sudo port dependents perl5

# see how much size each port occupies
port space --units MB --total ghostscript
# more detailed info
port contents --size depof:ghostscript

# see list of python versions installed
port select --list python
sudo port select --set python python27


```

```bash
# while port echo leaves also list the one which doesn't have dependencies, this script gives all the ports. difference between these two lists will give which are mainly installed via port install command.
list1=$(port echo leaves | cut -d'@' -f1)
list2=$(port installed | cut -d'(' -f1 | cut -d'@' -f1 | grep -v "following ports" | xargs port dependents | grep "has no dependents")
```

&nbsp;

For more commands see here. https://guide.macports.org/chunked/using.html

# Some packages I installed

Installed via Macports

|Tool|Description|
|encfs|EncFS is an encrypted pass-through filesystem using the FUSE kernel|
|sshfs|mounts filesystem on other remote system using ssh|
|sshpass|pass password for ssh protocol|
|pv|pipe viewer|

Installed via Homebrew

|Tool|Description|
|wget|Description|
|watch|Description|
|imagemagick|tools to manipulate images|
