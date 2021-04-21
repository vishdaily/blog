---
layout: page
title: Docker
categories: [computers]
tags: [docker, containers]
type: page
---

# Configure docker on ubuntu 18.04

```bash
sudo apt-get update
# it’s recommended to uninstall any old Docker software before proceeding.
sudo apt-get remove docker docker-engine docker.io
# install docker
sudo apt install docker.io
# Start and Automate Docker
sudo systemctl start docker
sudo systemctl enable docker
```
## About firewalls
Read about firewalls and docker
[https://docs.docker.com/network/iptables/]
If you want to learn in depth about firewalls in general
[https://www.netfilter.org/documentation/HOWTO/NAT-HOWTO.html]
[https://www.digitalocean.com/community/tutorials/how-to-list-and-delete-iptables-firewall-rules#:~:text=To%20flush%20a%20specific%20chain,sudo%20iptables%20%2DF%20INPUT]


### Logging dropped packets
[https://www.thegeekstuff.com/2012/08/iptables-log-packets/]

```bash
# Log All Dropped Packets (both Incoming and Outgoing)
iptables -N LOGGING
iptables -A INPUT -j LOGGING
iptables -A OUTPUT -j LOGGING
iptables -A LOGGING -m limit --limit 2/min -j LOG --log-prefix "IPTables-Dropped: " --log-level 4
iptables -A LOGGING -j DROP
```

In Ubuntu the logs are logged in /var/log/kern.log
Well, you can change the log location /etc/syslog.conf (kern.warning   /var/log/custom.log)
In other platforms, it might get logged to /var/log/messages

```bash
Aug  4 13:22:40 centos kernel: IPTables-Dropped: IN= OUT=em1 SRC=192.168.1.23 DST=192.168.1.20 LEN=84 TOS=0x00 PREC=0x00 TTL=64 ID=0 DF PROTO=ICMP TYPE=8 CODE=0 ID=59228 SEQ=2
Aug  4 13:23:00 centos kernel: IPTables-Dropped: IN=em1 OUT= MAC=a2:be:d2:ab:11:af:e2:f2:00:00 SRC=192.168.2.115 DST=192.168.1.23 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=9434 DF PROTO=TCP SPT=58428 DPT=443 WINDOW=8192 RES=0x00 SYN URGP=0
```
The dropped packets will be logged in the above format
Here is the explanation for each token.
- IPTables-Dropped: This is the prefix that we used in our logging by specifying –log-prefix option
- IN=em1 This indicates the interface that was used for this incoming packets. This will be empty for outgoing packets
- OUT=em1 This indicates the interface that was used for outgoing packets. This will be empty for incoming packets.
- SRC= The source ip-address from where the packet originated
- DST= The destination ip-address where the packets was sent to
- LEN= Length of the packet
- PROTO= Indicates the protocol (as you see above, the 1st line is for outgoing ICMP protocol, the 2nd line is for incoming TCP protocol)
- SPT= Indicates the source port
- DPT= Indicates the destination port. In the 2nd line above, the destination port is 443. This indicates that the incoming HTTPS packets was dropped


### Configuring firewalls for docker host system

```bash
apt-get install iptables-persistent
```

Everytime you modify firewalls make sure to save them using the following command.
Upon, reboot, these rules will be reloading. iptables-persistent package will ensure that. 

```bash
iptables-save > /etc/iptables/rules.v4
```

IMPORTANT::

If connecting remotely we must first temporarily set the default policy on the INPUT chain to ACCEPT otherwise once we flush the current rules we will be locked out of our server.
We used the -F switch to flush all existing rules so we start with a clean state from which to add new rules.
```bash
iptables -P INPUT ACCEPT
iptables -F
```

Docker inserts its own rules in to the iptables.
If you plan to open any ports and map them to localhost:3306 (for mysql), then this port is exposed to public
in order to block it from external access, modifying iptables is mandatory. 
Docker introduces new chain DOCKER-USER.
Before you do anything, make sure to run this, which deletes the default behaviour is to return.
It is also important to accept -o docker0 otherwise other containers cannot connect to mysql database

```bash
iptables -D DOCKER-USER -j RETURN
```
After this we would insert our own rules
```bash
iptables -P DOCKER-USER DROP
iptables -A DOCKER-USER -i lo -p all -j ACCEPT
iptables -A DOCKER-USER -o docker0 -j ACCEPT
iptables -A DOCKER-USER -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A DOCKER-USER -s 127.0.0.1 -j ACCEPT
iptables -A DOCKER-USER -p tcp -m tcp --dport 22 -j ACCEPT 
iptables -A DOCKER-USER -p tcp -m tcp --dport 80 -j ACCEPT 
iptables -A DOCKER-USER -p tcp -m tcp --dport 443 -j ACCEPT 
iptables -A DOCKER-USER -j DROP
```

Okay here is everything together.

```bash
# If connecting remotely we must first temporarily set the default policy on the INPUT chain to ACCEPT otherwise once we flush
iptables -P INPUT ACCEPT
iptables -F
# Before you do anything, make sure to run this, which deletes the default behaviour is to return.
iptables -D DOCKER-USER -j RETURN

# Create new chain called Logging
iptables -N LOGGING

iptables -P INPUT DROP
iptables -A INPUT -i lo -p all -j ACCEPT
iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A INPUT -s 127.0.0.1 -j ACCEPT
iptables -A INPUT -p tcp -m tcp --dport 45678 -j ACCEPT
iptables -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp -m tcp --dport 443 -j ACCEPT
# The below line is commented because, the packets that are not ACCEPTED from the above rules
# will be jumped to LOGGING policy where these will be logged, and finally DROPPED.
# if the below line is uncommented, the packets will not be propogated further
# iptables -A INPUT -j DROP
iptables -A INPUT -p tcp --dport 22 -m recent --update --seconds 600 --hitcount 3 --name SSH --rsource -j REJECT
iptables -A INPUT -p tcp --dport 22 -m recent --set --name SSH --rsource -j ACCEPT
# The first rule says that for any incoming connection on port 22, iptables first checks to see if this same IP address has already tried to connect 3+ times over the last 600 seconds. If it has, the newest incoming connection is rejected. 
# If it hasn't, the second rule is matched, accepting the connection.
iptables -A INPUT -j LOGGING
#iptables -P DOCKER-USER DROP
iptables -A DOCKER-USER -o eth0 -j ACCEPT
iptables -A DOCKER-USER -m conntrack --ctstate RELATED,ESTABLISHED -j RETURN
iptables -A DOCKER-USER -i lo -p all -j ACCEPT
iptables -A DOCKER-USER -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A DOCKER-USER -s 127.0.0.1 -j ACCEPT
# Accept only the ports to the outside world that are opened by docker
iptables -A DOCKER-USER -p tcp -m tcp --dport 443 -j ACCEPT
#iptables -A DOCKER-USER -j DROP
iptables -A DOCKER-USER -j LOGGING

iptables-save > /etc/iptables/rules.v4
```

### Commands
[https://www.tecmint.com/linux-iptables-firewall-rules-examples-commands/]



## Configure mysql
[https://stackoverflow.com/questions/47252273/unable-to-build-a-mariadb-base-in-a-dockerfile]
[https://github.com/dockerfile/mariadb/blob/master/Dockerfile]
[https://severalnines.com/blog/how-deploy-mariadb-server-docker-container]
[https://hub.docker.com/_/mariadb]
[https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux_atomic_host/7/html/getting_started_with_containers/install_and_deploy_a_mariadb_container]
[https://mariadb.com/resources/blog/try-mariadb-server-10-3-in-docker/]
[https://codeblog.dotsandbrackets.com/persistent-data-docker-volumes/]
[https://www.digitalocean.com/community/tutorials/how-to-share-data-between-the-docker-container-and-the-host]
[https://phoenixnap.com/kb/mysql-docker-container]
[https://mariadb.com/kb/en/installing-and-using-mariadb-via-docker/]
Well explained volume concept here
[https://stackoverflow.com/questions/41935435/understanding-volume-instruction-in-dockerfile]

```bash
mkdir -p /root/docker_data/mariadb_10_2/db/
# COPY the db data to the above location before running the container
```

```dockerfile
cat << EOF >> /root/docker_data/mariadb_10_2/Dockerfile
#cat /root/docker_data/mariadb_10_2/Dockerfile
FROM mariadb:10.2
#ENV MYSQL_ROOT_PASSWORD test123
#ENV MYSQL_DATABASE testDB
#ENV MYSQL_USER toto
#ENV MYSQL_PASSWORD test123
#RUN apt-get update && apt-get -y install vim
EXPOSE 3306
CMD ["mysqld"]
EOF
```

Then build your image

```bash
cd /root/docker_data/mariadb_10_2/Dockerfile
docker build -t mariadb_10_2 .
docker images
# make sure that old db data is present in /root/docker_data/mariadb_10_2/db
docker run --name mariadb_10_2 -ti -d -p 3306:3306 -v /root/docker_data/mariadb_10_2/db:/var/lib/mysql mariadb_10_2
docker ps
docker exec -it mariadb_10_2 bash
mysql -p -e "SHOW DATABASES;"
```

IMPORTANT:: If you want to connect to the db from other containers, make sure to grant access 
for the user to the DB from other hosts
```sql
GRANT ALL PRIVILEGES ON `DB_NAME`.* TO 'USER_NAME'@'%' ;
```

All commands are listed here
[https://severalnines.com/blog/how-deploy-mariadb-server-docker-container]

```bash
docker ps -a
docker stop mariadb_10_2
docker rm -v mariadb_10_2
docker ps -a
docker images
docker rmi mariadb_10_2
docker images
docker build -t mariadb_10_2 .
docker run --name mariadb_10_2 -ti -d -p 3306:3306 -v /home/vish/docker_data/ariadb_10_2/db:/var/lib/mysql mariadb_10_2
docker exec -it mariadb_10_2 bash
```

```bash
# Image search
docker search Image_Name
# Image download
docker pull Image_Name
# List the images installed
docker images
# List containers (adding the flag -a we can see also the stopped containers)
docker ps -a
# Delete a Docker Image
docker rmi Image_Name
# Delete a Docker Container (the container must be stopped)
docker rm Container_Name
# just rm doesnt remove the volume it created. -v option to also remove
# the volume
docker rm -v mariadbtest
# Run a container from a Docker Image (adding the flag -p we can mapping a container port to localhost)
docker run -d --name Container_Name -p Host_Port:Guest_Port Image_Name
# Stop container
docker stop --time=30 mariadbtest
docker kill mariadbtest
# Start container
docker start Container_Name
# Check container logs
docker logs Container_Name
# Check container information
docker inspect Container_Name
# Create a container linked
docker run -d --name Container_Name --link Container_Name:Image_Name Image_Name
# Connect to a container from localhost
docker exec -it Container_Name bash
# Create a container with volume added
docker run -d --name Container_Name --volume=/home/docker/Container_Name/conf.d:/etc/mysql/conf.d Image_Name
# Commit changes to a new image	
docker commit Container_ID Image_Name:TAG
# pausing
docker pause node1 node2 node3
docker unpause node1 node2 node3
# Remove all unused local volumes
docker volume prune
docker volume inspect
docker volume ls
docker volume rm
```

## Configure and setup apache
[https://hub.docker.com/_/httpd]

```bash
mkdir -p /root/docker_data/apache_2_4/public_html/
cat << EOF >> /root/docker_data/apache_2_4/public_html/index.html
Hello world from docker container
EOF
```

```dockerfile
cat << EOF >> /root/docker_data/apache_2_4/Dockerfile
FROM httpd:2.4
COPY ./public_html/ /usr/local/apache2/htdocs/
EOF
```

```bash
docker build -t apache_2_4 .
docker run -dit --name apache_2_4 -p 80:80 apache_2_4
```


### configure reverse proxy using apache2 on host system

[https://www.digitalocean.com/community/tutorials/how-to-use-apache-as-a-reverse-proxy-with-mod_proxy-on-ubuntu-16-04]

### wordpress
[https://stackoverflow.com/questions/35429920/access-to-mysql-container-from-other-container]
[https://www.howtoforge.com/tutorial/how-to-install-wordpress-with-docker-on-ubuntu/]
[https://severalnines.com/database-blog/mysql-docker-containers-understanding-basics]


### nextcloud
[https://www.techrepublic.com/article/how-to-install-nextcloud-16-on-ubuntu-18-04/]

[https://www.codeooze.com/ubuntu/ubuntu-18-docker-apache/]

[https://github.com/dhanugupta/docker-apache-ubuntu/blob/master/Dockerfile]

```dockerfile
FROM ubuntu:latest

RUN apt-get update
RUN apt-get -y upgrade


```


## Debug

https://medium.com/@pimterry/5-ways-to-debug-an-exploding-docker-container-4f729e2c0aa8
