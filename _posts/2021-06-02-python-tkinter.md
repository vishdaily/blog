---
title: All about GPG keys
layout: post
tags:
  - python
  - tkinter
---

Tkinter is Python's de-facto standard GUI (Graphical User Interface) package. It is a thin object-oriented layer on top of Tcl/Tk according to https://wiki.python.org/moin/TkInter

# Setting up on mac

Well i should say that setting up it on mac is such a pain. May be i din't understand it completely.

After googling, i started with 

```bash
brew upgrade tcl-tk
```

The following information appeared during installation suggests that, I should set these variables
to successfully run the tkinter program 

```bash
tcl-tk is keg-only, which means it was not symlinked into /usr/local,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.

If you need to have tcl-tk first in your PATH, run:
  echo 'export PATH="/usr/local/opt/tcl-tk/bin:$PATH"' >> /Users/vish/.bash_profile

For compilers to find tcl-tk you may need to set:
  export LDFLAGS="-L/usr/local/opt/tcl-tk/lib"
  export CPPFLAGS="-I/usr/local/opt/tcl-tk/include"

For pkg-config to find tcl-tk you may need to set:
  export PKG_CONFIG_PATH="/usr/local/opt/tcl-tk/lib/pkgconfig"
```

After setting the above variables, then install python version using pyenv. There are various ways of making it work. But the following worked for me.

```bash
# It is important to mention the Tcl/tk version as 8.6 before installing. 
PYTHON_CONFIGURE_OPTS="--with-tcltk-includes='-I/usr/local/opt/tcl-tk/include' --with-tcltk-libs='-L/usr/local/opt/tcl-tk/lib -ltcl8.6 -ltk8.6'" pyenv install 3.8.3
```

Reference : https://github.com/pyenv/pyenv/pull/1397
