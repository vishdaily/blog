---
layout: page
title: Linux Commands
categories: [linux]
tags: [linux]
type: page
---

### uname
```bash
uname -a
```

### rpm2cpio
```bash
rpm2cpio VirtualBox-5.0-5.rpm | cpio -idmv
```
### rpm

```bash
# display contents of rpm package
rpm -qli /tmp/<rpm_package_name>.rpm

rpm -qa | grep php

rpm -qf /etc/yum.repos.d/epel.repo

# list the contents of rpm pacakge 
rpm -qlp kabana.rpm

rpm -qa | grep php | yum -y remove

# This will list where to package will extracts the files to upon installation 
rpm -ql php70w-7.0.18-1.w7.x86_64
```


### yum

```bash
yum list installed
yum remove < package name>
yum grouplist
yum repolist
yum groupinfo "Development Tools" | less
yum --showduplicates list kernel 
yum search kernel
yum history list 244
yum history info 244
yum localinstall /tmp/local.rpm
# if the yum database is not up to date or some errors like 
yum clean all
yum repolist all | grep mysql
yum clean metadata
yum list installed mariadb\*
yum --disablerepo="*" --enablerepo="epel" list available | grep <package>
# Yum Lock Package Version At a Particular Version
yum versionlock package1 package2
```