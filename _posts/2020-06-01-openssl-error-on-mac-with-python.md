---
title: pyhton pip SSL module is not available on mac problem
layout: post
tags:
  - mac
  - python
  - openssl
---

Before anything, if you have updated OSx recently, run from command line
```bash
xcode-select --install
brew doctor
brew update
brew upgrade
```


A BIG NOTE::

brew install openssl1.1, but only few python versions have openssl1.1 others while others have OpenSSL 1.0.2 according to this post
[https://github.com/pyenv/pyenv/issues/1425#issuecomment-582204245]
> OpenSSL 1.1.0 support in the ssl module was only added to Python 2.7.13, 3.5.3 and 3.6.0 ...

If you want to compile any other python version, then you have to download and compile OpenSSL 1.0.2 and manually link it 
[https://stackoverflow.com/questions/38670295/homebrew-refusing-to-link-openssl] and later remove it.

