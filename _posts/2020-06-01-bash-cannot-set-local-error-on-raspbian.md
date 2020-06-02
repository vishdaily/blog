---
title: Cannot set locale on raspbian
layout: post
tags:
  - raspbian
  - raspberrypi
---

In case of following warnings on raspbian os
```bash
bash: warning: setlocale: LC_ALL: cannot change locale (en_US.UTF-8)
bash: warning: setlocale: LC_ALL: cannot change locale (en_US.UTF-8)
bash: warning: setlocale: LC_ALL: cannot change locale (en_US.UTF-8)
bash: warning: setlocale: LC_ALL: cannot change locale (en_US.UTF-8)
```

Edit the default locale:
```bash
vim /etc/default/locale
```

Add
```bash
LANGUAGE=en_US.UTF-8
LANG=en_US.UTF-8
LC_ALL=en_US.UTF-8
```

Run
```bash
locale-gen en_US.UTF-8
dpkg-reconfigure locales
```