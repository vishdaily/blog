---
layout: page
title: Letsencrypt
categories: [ssl]
tags: [letsencrypt, ssl]
type: page
---


# Add new sub domain to the certificate

There is no certbot command to just add the new subdomain. We have to mention all the domains including the old one's.

To see the list of all certificates, use 'certbot certificates' command

Then use the following command to recreate / renew the certificate using the new-subdomain

Note: Using the standalone server option to verify the domain names requires port 80 to be free. Which means, if you already have a apache running on this port, make sure that apache is stopped to use standalone option. 

```bash
root@server# certbot certificates
Saving debug log to /var/log/letsencrypt/letsencrypt.log

-------------------------------------------------------------------------------
Found the following certs:
  Certificate Name: example.com
    Domains: example.com subdomain1.example.com
```

Use -d parameter to include all the domains including old domains and the new one too

```Bash
/usr/bin/certbot certonly -d example.com -d subdomain1.example.com -d new-subdomain.vishdaily.com

Saving debug log to /var/log/letsencrypt/letsencrypt.log

How would you like to authenticate with the ACME CA?
-------------------------------------------------------------------------------
1: Apache Web Server plugin - Beta (apache)
2: Spin up a temporary webserver (standalone)
3: Place files in webroot directory (webroot)
-------------------------------------------------------------------------------
Select the appropriate number [1-3] then [enter] (press 'c' to cancel): 2
Plugins selected: Authenticator standalone, Installer None

```

# Alternate approach instead of renewing all the subdomains

If you were using the above approach, then delete all the sub domains. 
Later you can individually create certicates for each
```bash
/usr/bin/certbot delete sub1.maindomain.com
/usr/bin/certbot delete sub2.maindomain.com
```
Stop the running apache server

Then renew the certificates
```bash
certbot certonly -d maindomain.com
certbot certonly -d sub1.maindomain.com
```

# letsencrypt on ubuntu 20

```bash
apt install letsencrypt
systemctl status certbot.timer
# ensure that no port is running on 80
certbot certonly --standalone --agree-tos --preferred-challenges http -d domain-name.com
```