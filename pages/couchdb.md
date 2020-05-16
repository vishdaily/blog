---
layout: page
title: CouchDB
categories: [databases]
tags: [couchdb, databases]
type: page
---

# CouchDB-2.3.1

## Installation on Ubuntu 16.04

[https://docs.couchdb.org/en/2.2.0/install/index.html](https://docs.couchdb.org/en/2.2.0/install/index.html)

```bash
echo "deb https://apache.bintray.com/couchdb-deb xenial main" \ | sudo tee -a /etc/apt/sources.list
curl -L https://couchdb.apache.org/repo/bintray-pubkey.asc \ | sudo apt-key add -
apt-cache madison couchdb
apt-get install couchdb=2.3.1~xenial
```

Add admin user / udpate admin user password

```bash
systemctl stop couchdb

vim /opt/couchdb/etc/local.ini
# Edit local.ini file under [admins] add
# user = password
# after restart of couchdb the password will be encrypted in this file and user is created
systemctl start couchdb
```

## Secure Couch DB: Setup SSL

You will need the OpenSSL command line tool installed. It probably already is.

```bash
mkdir /etc/couchdb/cert
cd /etc/couchdb/cert
openssl genrsa > privkey.pem
openssl req -new -x509 -key privkey.pem -out couchdb.pem -days 1095
chmod 600 privkey.pem couchdb.pem
chown couchdb privkey.pem couchdb.pem
```

Now, you need to edit CouchDB’s configuration, by editing your /opt/couchdb/etc/local.ini file. Here is what you need to do.

Under the [ssl] section, enable HTTPS and set up the newly generated certificates:

```bash
[ssl]
enable = true
cert_file = /etc/couchdb/cert/couchdb.pem
key_file = /etc/couchdb/cert/privkey.pem
```

### When using letsencrypt

In order to use letsencrypt certificates for couchdb ssl, cacert_file option also needs to be enabled.

Copy letsecrypt certificates from /etc/letsecrypt/archive/.. folder to /etc/couchdb/cert/ and make sure that permissions are set to 600

```bash

# Note that the file names can be different. verify the actual certificates using openssl x509 -text -no-out -in command

# FROM 
/etc/letsencrypt/archive/example.com-0001/cert6.pem
/etc/letsencrypt/live/example.com-0001/privkey6.pem
/etc/letsencrypt/live/example.com-0001/chain6.pem

# TO
/etc/couchdb/cert/cert.pem
/etc/couchdb/cert/privkey.pem
/etc/couchdb/cert/chain.pem

chmod 600 /etc/couchdb/cert/*.pem
chown couchdb:root /etc/couchdb/cert/*.pem
```

Set the following options in local.ini

```bash
# vi /opt/couchdb/etc/local.ini

[ssl]
enable = true
cert_file = /etc/couchdb/cert/cert.pem
key_file = /etc/couchdb/cert/privkey.pem
cacart_file = /etc/couchdb/cert/chain.pem
```

```bash
cp /etc/letsencrypt/archive/vishdaily.com-0001/cert9.pem cert.pem
cp /etc/letsencrypt/archive/vishdaily.com-0001/chain9.pem chain.pem
cp /etc/letsencrypt/archive/vishdaily.com-0001/privkey9.pem privkey.pem

systemctl restart couchdb
```

### Secure Couch DB: Avoid epmd and beam.smp binding 4369 on public interface

After installation epmd and beam.smp make port available for public. This is not required if you just want to use it locally. To avoid this

To make beam.smp listen to localhost

```bash
# Add the following line in /opt/couchdb/etc/vm.args at the end
-kernel inet_dist_use_interface 127.0.0.1
```

To make epmd listen to localhost

```bash
# Add the following line in /opt/couchdb/bin/couchdb before exec "$BINDIR/erlexec" 
export ERL_EPMD_ADDRESS="127.0.0.1"
```

Ref: https://github.com/apache/couchdb/issues/999

*Important* For the above setting to work, make sure that IPV6 is enabled atleast for loopback interface (lo). This can be set in /etc/sysctl.conf and restart the system.

```bash
net.ipv6.conf.lo.disable_ipv6=0
```

Ref: http://erlang.2086793.n4.nabble.com/epmd-regression-bug-in-erlang-solutions-com-esl-erlang-18-3-td4716411.html

### Secure Couch DB: Tips

#### Add users to all databases

You need to set each database security object and add members in the 'members' and 'admins' field. It is important to assign users to all databases including _users and _replications. Databases without user permissions would be accessible without authentication !!

Also set require_valid_user=true in local.ini

Ref: https://docs.couchdb.org/en/stable/config/auth.html

```bash
[httpd]
WWW-Authenticate = Basic realm="administrator"
require_valid_user = true

[couch_httpd_auth]
require_valid_user = true
```

#### Change the default port numbers

Change port numbers in /opt/couchdb/etc/local.ini and restart couchdb

```bash
[chttpd]
port = xxxxx

[ssl]
port = xxxxx
```

#### Enable only https

Seems to be that we cannot blog http. Work around is to block insecure port https://github.com/apache/couchdb/issues/901

### Project Fauxton is a web interface running under

http://127.0.0.1:5984/_utils

https://127.0.0.1:6984/_utils

admin/admin

### User Creation
https://docs.couchdb.org/en/2.2.0/intro/security.html

Create New User

```bash
curl -X PUT http://localhost:5984/_users/org.couchdb.user:jan \
     -H "Accept: application/json" \
     -H "Content-Type: application/json" \
     -d '{"name": "jan", "password": "apple", "roles": [], "type": "user"}'
```

## Export and Import Databases
Database can be exported to JSON using the following REST API URL

```bash
curl -X GET http://127.0.0.1:5984/noteself/_all_docs?include_docs=true > ~/Downloads/noteself.json
```

The resulting JSON looks like this

```bash
{
  "total_rows": 34,
  "offset": 0,
  "rows": [
    {
      "id": "linux",
      "key": "linux",
      "value": {
        "rev": "1-3d26a00b306c1482b2f7e4e8bdb0549f"
      },
      "doc": {
        "_id": "linux",
        "_rev": "1-3d26a00b306c1482b2f7e4e8bdb0549f",
        "fields": {
          "created": "20190719223255819",
          "creator": "admin"
        }
      }
    },
        {
      "id": "linux",
      "key": "linux",
      "value": {
        "rev": "1-3d26a00b306c1482b2f7e4e8bdb0549f"
      },
      "doc": {
        "_id": "linux",
        "_rev": "1-3d26a00b306c1482b2f7e4e8bdb0549f",
        "fields": {
          "created": "20190719223255819",
          "creator": "admin"
        }
      }
    }
  ]
}
```
In order to be importable, it is important to remove _rev, total_rows etc attributes from the json formed from the above step. The above json file should be edited such that it has the following format. 

```bash
{"docs": [
  {
    "_id": "linux",
    "fields": {
      "created": "20190719223255819",
      "creator": "admin",
      "title": "Linux",
      "modified": "20190719223255819",
      "modifier": "admin",
    }
  },
  {
    "_id": "windows",
    "fields": {
      "created": "20190719223255819",
      "creator": "admin",
      "title": "Windows",
      "modified": "20190719223255819",
      "modifier": "admin",
    }
  }
]
}
```

Following one liner can be used to achieve the desired output

```bash
cat noteself.json | jq '.rows[].doc' | jq -s '.' | grep -v _rev > noteself_to_import.json
```

The resulted json from the above step can be imported with curl

```bash
curl -X POST -H "Content-Type: application/json" -d @noteself_to_import.json -u user:pass http://127.0.0.15984/my_new_database/_bulk_docs
```

## CouchDB FAQs
### What is beam.smp process 

https://developer.couchbase.com/documentation/server/3.x/admin/Monitoring/monitor-underlying-processes.html

### Where are CouchDB databases stored on file system

#### Mac
~/Library/Application Support/CouchbaseServer

#### Linux
/var/lib/couchdb/