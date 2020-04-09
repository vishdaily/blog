---
id: 243
title: Run service on startup in mac
date: 2017-05-23T21:00:04+00:00
author: vish
layout: post
guid: https://blog.vishdaily.com/?p=243
permalink: /index.php/computers/mac/run-service-on-startup-in-mac/
post_icon:
  - mac-osx.png
categories:
  - Mac
tags:
  - mac
---
In the following code, i am starting my apache during the startup.

Create a file /Library/LaunchDaemons/apachefriends.xampp.apache.start.plist

```bash
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
    <key>EnableTransactions</key>
    <true/>
    <key>Label</key>
    <string>apachefriends.xampp.apache.start</string>
    <key>ProgramArguments</key>
    <array>
        <string>/Applications/XAMPP/xamppfiles/xampp</string>
        <string>startapache</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>WorkingDirectory</key>
    <string>/Applications/XAMPP/xamppfiles</string>
    <key>KeepAlive</key>
    <false/>
    <key>AbandonProcessGroup</key>
    <true/>
    </dict>
</plist>

```

&nbsp;