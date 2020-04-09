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

<pre class="lang:xhtml decode:true ">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd"&gt;
&lt;plist version="1.0"&gt;
&lt;dict&gt;
	&lt;key&gt;EnableTransactions&lt;/key&gt;
	&lt;true/&gt;
	&lt;key&gt;Label&lt;/key&gt;
	&lt;string&gt;apachefriends.xampp.apache.start&lt;/string&gt;
	&lt;key&gt;ProgramArguments&lt;/key&gt;
	&lt;array&gt;
		&lt;string&gt;/Applications/XAMPP/xamppfiles/xampp&lt;/string&gt;
		&lt;string&gt;startapache&lt;/string&gt;
	&lt;/array&gt;
	&lt;key&gt;RunAtLoad&lt;/key&gt;
	&lt;true/&gt;
	&lt;key&gt;WorkingDirectory&lt;/key&gt;
	&lt;string&gt;/Applications/XAMPP/xamppfiles&lt;/string&gt;
	&lt;key&gt;KeepAlive&lt;/key&gt;
	&lt;false/&gt;
	&lt;key&gt;AbandonProcessGroup&lt;/key&gt;
	&lt;true/&gt;
&lt;/dict&gt;
&lt;/plist&gt;
</pre>

&nbsp;