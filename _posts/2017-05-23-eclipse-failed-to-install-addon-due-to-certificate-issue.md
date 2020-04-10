---
id: 257
title: Eclipse failed to install addon due to certificate issue
date: 2017-05-23T13:07:40+00:00
author: vish
layout: post
guid: https://blog.vishdaily.com/?p=257
permalink: /index.php/computers/developer-tools/eclipse-failed-to-install-addon-due-to-certificate-issue/
post_icon:
  - eclipse.png
categories:
  - developer-tools
tags:
  - eclipse
  - java-certificates
---
In my case I wanted to install subclipse, the eclipse market place is trying to connect to <https://dl.bintray.com/> but resulting in to certificate error due to bad domain name. True it could be some fake sites pretending to be the trusted. But in this case, i know that this is this exact site.

<span style="font-family: 'courier new', courier, monospace;">&#8220;sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target&#8221;</span>

Solution is to :

Download this certificate (I did it using chrome -> export functionality)

Add the certificate to cacerts (server trust store for java)

```bash
keytool -import -noprompt -trustcacerts -alias proxy_certficate -file /tmp/CertificateToBeTrusted  -keystore /etc/pki/ca-trust/extracted/java/cacerts -storepass changeit
```