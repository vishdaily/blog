---
title: Install custom packages on qnap
layout: post
tags:
  - internet
  - qnap
  - nas
---

Download and install Entware package as described in 
[https://github.com/Entware/Entware/wiki/Install-on-QNAP-NAS]

Login as admin 

The entware package would be installed in the path
/opt/bin

Run /opt/bin/Entware.sh which will move all the files to a saperate dir and links /opt to the target directory. This script also make all the commands installed via opkg in the user PATH

## Install screen

```bash
/opt/bin/opkg --help
/opt/bin/opkg install screen
```

Running the screen might give the following errors initially

```bash
/var/run/utmp: No such file or directory
Cannot find terminfo entry for 'xterm-color'.
```

Workaround
```bash
touch /var/run/utmp; # fix missing file
export TERMINFO=/opt/share/terminfo; # set missing environment variables for TERM
```





