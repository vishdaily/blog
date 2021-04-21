---
title: install pyaudio on python 2.7.13 to manipulate audio using python
layout: post
tags:
  - python
  - raspberrypi
---

```bash
apt-get install --no-install-recommends make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
apt-get install python-openssl
apt-get install -y build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl git
# Assuming that pyenv is setup
pyenv install -v 2.7.13
pyenv virtualenv 2.7.13 2_7_13
pyenv local 2_7_13

# Important 
apt-get install portaudio19-dev

python -m pip install pyaudio
```
bento