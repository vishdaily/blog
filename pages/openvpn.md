---
layout: page
title: German Language
categories: [internet]
tags: [openvpn]
type: page
---

## OpenVPN on Ubuntu 18.04

This setup uses Ubuntu 18.04 as base OS

References:

https://linuxconfig.org/openvpn-setup-on-ubuntu-18-04-bionic-beaver-linux#h3-difficulty

https://www.digitalocean.com/community/tutorials/how-to-set-up-an-openvpn-server-on-ubuntu-18-04

NAT VPN https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_72/rzaja/rzajavpnnat.htm

```bash
# To see list of all clients connected
killall -USR2 openvpn ; tail -f /var/log/syslog
# kill openvpn gracefully
pkill -SIGTERM -f 'openvpn --daemon --conf $OPENVPNCONFFILE' 
```

Installing the Client Configuration

Windows, download openvpn client from openvpn.org

Mac, Tunnelblick is free can be downloaded from

https://tunnelblick.net/downloads.html

Tunnelblick path on Mac

~/Library/Application Support/Tunnelblick

```bash
apt install openvpn
# on ubuntu check if /etc/openvpn/update-resolv-conf pressent, if yes then the following is valid
cp /tmp/client.ovpn /etc/openvpn/client.ovpn
# vim /etc/openvpn/client.ovpn
# Add the following lines 

#script-security 2
#up /etc/openvpn/update-resolv-conf
#down /etc/openvpn/update-resolv-conf

# On centOS
# group nobody

openvpn --config /etc/openvpn/client1.ovpn
```

### How to list clients connected to openvpn

added the following in /etc/openvpn/server.conf

```bash
management localhost 7505
# restart. later you can connect to telnet
telnet localhost 7505
# to see all the commands type help
# to see the status or clients connected type
status

```

### Generate Client Certificate

```bash
cd /data/certificates/
source vars && ./build-key client-vishqnap
clients/make_config.sh client-vishqnap
```

### Revoke Client Certificates

#### Things to note before revoking certificates

https://anton.dollmaier.name/2019/07/08/openvpn-crl-has-expired.html

Change default_crl_days=30 to default_crl_days=3650. Otherwise you will face error depth=0 error=crl has expired.. when ever you are connecting to vpn client. And the connection fails. 

#### Here is how to Revoke the Certificates

Reference - https://blog.stigok.com/2017/12/28/openvpn-revoke-client-certificate.html https://openvpn.net/community-resources/revoking-certificates/

```bash
cd /data/certificates
source vars
./revoke-full client-vishqnap
cat keys/index.txt
openssl crl -in keys/crl.pem -text
cp keys/crl.pem /etc/openvpn/
# vim /etc/openvpn/server.conf
# Ensure the following is present 
# crl-verify /etc/openvpn/crl.pem
# /etc/init.d/openvpn reload
```

