---
layout: page
title: Linux Commands
categories: [linux]
tags: [linux]
type: page
---

### awk
```bash
#&amp;nbsp;https://www.gnu.org/software/gawk/manual/gawk.html
# http://www.thegeekstuff.com/2010/01/8-powerful-awk-built-in-variables-fs-ofs-rs-ors-nr-nf-filename-fnr/?ref=binfind.com/web

grep "as root on" output.log | awk '{ print substr( $0, length($0) -11, length($0))}'
# awk used here to print the string of words in reverse order. Then split them with space as delimeter. Prints the third value which is number. Finally Sums all the numbers and displays the sum
grep 'Testcases passed' testobjects.txt | awk '{ for (i=NF; i&gt;1; i--) printf("%s ", $i); print $1; }' | awk '{split($0,a," "); print a[3]}' | awk '{ SUM+= $1 } END { print SUM }'
# substring
grep "as root on" output.log | awk '{ print substr( $0, length($0) -11, length($0))}'
# split string
echo "test|temp|dot|com" | awk '{split($0,a,"|"); print a[2],a[3],a[1]}'
# skip 29 lines after matching the string
cat /tmp/test.log | awk -v nlines=29 '/Unable to process Jar entry/ {for (i=0; i&lt;nlines; i++) {getline}; next} 1' |  sed '/^\s*$/d' 
# format text
grep host_group /tmp/test.log | awk -F' ' '{printf "%-20s %-40s\n", $2,$4;}'
# pass shell variables to awk
awk -v a="$var1" -v b="$var2" 'BEGIN {print a,b}'
# windows to unix conversion
awk '{ sub("\r$", ""); print }' winfile.txt &gt; unixfile.txt
# unix to windows conversion
awk 'sub("$", "\r")' unixfile.txt &gt; winfile.txt
```

### cat
```bash
cat /etc/passwd | cut -d: -f2
p=$(cat /proc/1336/environ | tr '\0' '\n'
```

### crontab
```bash
# http://www.thegeekstuff.com/2009/06/15-practical-crontab-examples/

crontab -l
crontab -e
crontab -u test -e

# run the CMD every minute 
* * * * * CMD

# every 10 minutes 
*/10 * * * * CMD

@yearly 0 0 1 1 *
@daily 
@hourly 0 * * * *
@reboot Run at startup.
```

### curl
```bash
# make POST request with params and http basic authentication
curl -k -s -u admin:pass -H 'Accept: application/json' -X POST 'https://localhost:4444/testing' -d '{ "type": "Service", "filter": "match(\"testing\", search_expression)", "another_param": value }' | python -m json.tool
```

### date
```bash
# https://www.cyberciti.biz/tips/linux-unix-get-yesterdays-tomorrows-date.html
date +"%d_%m_%Y"
date --date="yesterday" 
yesterday=$(date --date="yesterday" +"%d_%m_%Y")
```

### dig
```bash
dig -x www.google.com
```

### dmesg
```bash
# dmesg command is used to write the kernel messages in Linux to standard output
dmesg
```

### dnsdomainname
```bash
dnsdomainname    # displays the domain name of the server
```

### echo
```bash
echo $HISTFILESIZE

# display current shell
echo $SHELL
echo $0
```

### find
```bash
find . -type f -name "test*"

find . -type d -name "localhost*"

# find lolcat in any dir except cygdrive and drives
find . -type d \( -name cygdrive -o -name drives \) -prune -o -name "lolcat*" -print

find . -type f | xargs chmod 644

# Use the prune switch, for example if you want to exclude the misc directory just add a -path ./misc -prune -o
find . -path ./misc -prune -o -name '*.txt' -print

find . -type d \( -path dir1 -o -path dir2 -o -path dir3 \) -prune -o -print

find -L &lt;dir&gt;  # navigate through all folders

# Delete all files except .txt files
find . ! -name '*.txt' -type f -exec rm -f {} \;
```

### getent
```bash
getent group git
getent hosts www.google.com
```

### gpasswd
```bash
# gpasswd is used to administer /etc/group an /etc/gshadow
# adds tom user to group users
gpasswd -a tom users
```

### gpg
```bash
# https://www.gnupg.org/
gpg --gen-key
gpg --verify &lt;key&gt;
gpg --edit-key testing@gmail.com
&gt;&gt;&gt;&gt; fpr
&gt;&gt;&gt;&gt; sign
&gt;&gt;&gt;&gt; check
gpg --fingerprint
gpg --list-keys
gpg --list-secret-keys
gpg --full-generate-key
gpg --export -o testing.pub -r testing@gmail.com
gpg -o 1 1.raw
gpg --yes 11.raw
gpg --change-passphrase testing@gmail.com
gpg --export --armor -o "testing@gmail.com.pubring.gpg" -rtesting@gmail.com
gpg --armor -o "testing@gmail.com.privring.gpg" --export-secret-key testing@gmail.com
gpg --output doc.gpg --encrypt --recipient blake@cyb.org doc
gpg --output doc --decrypt doc.gpg
gpg --output doc.gpg --symmetric doc
```

### grep
```bash
grep VirtualHost *conf

grep ErrorLog vhost_0_localhost.conf

# Stop reading the file after num matches.
grep -m 1 VirtualHost *conf --color=auto

# case insensitive search
grep -i VirtualHost *conf --color=auto

grep -nwr . --include="*.conf" -e '-Djava.net.preferIPv4Stack=true"' --color=auto

# Find the string given by expression -e, display line number include only files ending with conf
grep 'CATALINA_OPTS="${CATALINA_OPTS} -dheap"' tomcat7.conf.bak --color=auto

# grep all the entries what is not GET 
grep -v GET access.log

# grep recursively for 443 
grep -r --include="*" '443' /etc/httpd

# grep for multiple patterns 
grep 'foo\|bar' *.txt, grep -E 'foo|bar' *.txt, grep -e foo -e bar *.txt

#  grep for items starting with and not contain a perticular string
# -E is not working in cygwind. so use -P
grep -r -i -E 'index = (?!.*patter1|.*pat3|.*pattern2|.*pat4|.*pat5)' ./*/dump/*.conf

# 
grep -E '^[^#].*searchstring|^[^#].*environment' file
```

### groupdel
```bash
groupdel  git_users
```

### groups
```bash
groups test
```

### gzip
```bash
gzip zip_this_file.log

# find all the files except skip_this_log.log and gzip them 
find -type f -not -name "skip_this_log.log" -exec gzip {} \;
```

### htpasswd
```bash
htpasswd /etc/httpd/conf.d/svn.users svnuser
```

### iconv
```bash
iconv -f ascii -t utf8 [filename] &gt; [newfilename]
iconv -f utf8 -t ascii [filename]
```

### jq
```bash
# 
jq '.results[0].attrs.__name' test.json
#fetch multiple attributes
jq '.results[].attrs | "\(.__name)|\(.active)|\(.last_check_result.state)|\(.last_check_result.output)"' test.json
# sort based on key name
cat objects.json | jq -S 'sort_by(.object_name)'
# select items based on key=value ## [{"id": "first", "val": 1}, {"id": "second", "val": 2}]
jq '.[] | select(.id == "second")'
# create json from extracted values
cat objects.json | jq '. | {name: .object_name, type: .object_type}'
# create valid json from unproper json (normally json objects with out , at the end
cat objects.json | jq . -s
# extract information from json and convert to csv
jq -r '.results | map([.attrs.__name, .attrs.active, .attrs.last_check_result.state] | @csv) | join("\n")']
```

### jstat
```bash
#  java garbage collection statistics
su tomcat -c "/usr/lib/jvm/java-1.6.0-openjdk.x86_64/bin/jstat -gcutil 27672"
su tomcat -c "/usr/lib/jvm/java-1.6.0-openjdk.x86_64/bin/jstat -gccapacity 27672"
```

### keytool
```bash
# list the certifacates in the keystore
echo 'changeit' | keytool -list -keystore /tmp/server.truststore
keytool -list -storepass changeit -keystore /tmp/server.truststore

# import the certifcatre to the keystore 
keytool -import -file my.cert.location/my.cert.crt -storepass changeit -keystore $JAVA_HOME/jre/lib/security/cacerts

# export a perticular certificate from keystore 
keytool -exportcert -storepass changeit -keystore $JAVA_HOME/jre/lib/security/cacerts -alias mycert1 &gt; my.cert.location/my.cert.1.crt

# just print the certificate details 
keytool -printcert -file mycert.crt

# deelte the certificate from the keystore 
keytool -delete -storepass changeit -keystore $JAVA_HOME/jre/lib/security/cacerts -alias mycert1

# no prompt useful in bash script. 
keytool -delete -storepass changeit -keystore $JAVA_HOME/jre/lib/security/cacerts -alias mycert1 -noprompt

# If you want to use openssl s_client with the certs from that keystore, you can extract them into a usable form with
keytool -list -rfc -keystore /etc/ssl/certs/java/cacerts &gt; cacerts.pem
```

### kill
```bash
# send a signal to generate the thread dump. it doesn't kill the process. tid is the thread id, nid is the native thread id in the os. you can look it inside the log.
kill -3 34333

# sends a signal to OS to kill the process. SIGKILL 
kill -9

# sends a signal to the process requesting to kill itself.. SIGTERM 
kill -15
```

### killall
```bash
killall -9 -u techmint    # kill all the processes of the user techmint
```

### ldapsearch
```bash
ldapsearch -P 3 -H "ldap://hostname:3268" -D "CN=USERID,OU=L,OU=Useraccounts,OU=??,DC=??,DC=?????,DC=???" -W -b "CN=&lt;&lt;LDAPGROUP&gt;&gt;,OU=LOCALGROUPS,OU=SECURITYGROUPS,OU=??,DC=??,DC=?????,DC=???"
```

### lftp
```bash
lftp -u login,password -e "put $THEFOLDER/$file;quit" theftp/sub/folder
lftp -u user,password ip_address
```

### lsmod
```bash
# It shows which loadable kernel modules are currently loaded.
lsmod | grep vbox
```


### modprobe
```bash
# modprobe intelligently adds or removes a module from the Linux kernel
modprobe -I vboxvideo
modprobe -h
```

### mount
```bash
# For cent OS, sr0 is the cd rom
mount /dev/sr0 /mnt

mount -o loop VBoxGuestAdditions.iso /mnt/

mount -t nfs4 -o ro &lt;nfs_dir&gt;:/vol/dir/testdir/ /data/testdir
```

### openssl
```bash
# https://www.madboa.com/geek/openssl/
# https://www.openssl.org/docs/manmaster/apps/

# Display Certificate Details or Decode certificate
openssl x509 -in /etc/pki/tls/certs/testcertificate.crt -text -noout

openssl x509 -in TrustedSecureCertificateAuthority5.crt -noout -sha1 -fingerprint
openssl x509 -in TrustedSecureCertificateAuthority5.crt -noout -sha256 -fingerprint

# Display fingerprint of the certificate via sha1 or sha256 or md5 checksum hashes.
openssl x509 -in TrustedSecureCertificateAuthority5.crt -noout -md5 -fingerprint

# Decode a key
openssl rsa -text -in private/testcertificate.key

# Decode csr (Certificate Sign Request) 
openssl asn1parse -in &lt;csr-file&gt;

# Decode certificate from request 
openssl s_client -connect example.com:443

# Get the matching public key from the private key 
openssl rsa -pubout -in private/testcertificate.key

# Get the matching public key from the certificate 
openssl x509 -noout -pubkey -in certs/testcertificate.crt

# Create self signed certificate 
openssl req -x509 -new -newkey rsa:2048 -nodes -keyout myselfsigned.key -out myselfsigned.crt -subj '/C=IN/ST=AP/L=Bangalore/O=Self/CN=www.mydomain.de'

# Create self signed certificate 10 years valid. 
openssl req -x509 -new -newkey rsa:2048 -nodes -days 3650 -keyout selfsigned_certificate.key -out selfsigned_certificate.crt -subj '/C=IN/ST=AP/L=Bangalore/O=Self/CN=www.mydomain.de'

# another self signed certificate. fill details after 
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout localhost_custom.key -out localhost_custom.crt

openssl req -x509 -new -days 365 -newkey rsa:2048 -nodes -keyout localhost_custom.key -out localhost_custom.crt -subj '/C=IN/ST=AP/L=Bangalore/O=Self/CN=www.mydomain.de'
```

### passwd
```bash
(echo 'NewPassword'; echo 'NewPassword') | passwd testuser

# lock user
passwd --lock tecmint
```

### pgrep
```bash
pgrep -u techmint     # find out all running processses of user account
```

### printf
```bash
printf "%*s" $COLUMNS | tr " " "-"
```

### ps
```bash
ps -f --pid ${pgrep -u techmint}
ps -mo pid,lwp,time -C java # display threads ids of a perticular command for example here java
ps -mo pid,lwp,time -p 23343 # by process
ps fax # show the process and subprocesses in a tree like view
ps -eo pid,ppid,cmd,%mem,%cpu
```

### pwdx
```bash
# using pwdx find out the current working directory of the process 3813
pwdx 3813
```

### repoquery
```bash
# query information from yum repositories.
repoquery -q -l —plugins ksh
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

### rpm2cpio
```bash
rpm2cpio VirtualBox-5.0-5.rpm | cpio -idmv
```

### rsync
```bash
rsync --dry-run --delete --exclude=temp/ -aAXzve ssh $username@$server:$src_dir $trg_dir
rsync --dry-run --delete --exclude=*skip_backup/ -aAXzv /drives/c/dev/ /drives/u/backup/

# with dry run exclude svn files
rsync -avzn --delete -exclude '.svn*' /tmp/sizzleup/ ~/Documents/workspaces/workspace-sts-3.8.1.RELEASE/project1/

rsync -avz --delete -exclude '.svn*' /tmp/sizzleup/ ~/Documents/workspaces/workspace-sts-3.8.1.RELEASE/project1/
```

### screen
```bash
screen -S name1
screen -ls
screen -r name1
screen -r
screen -r 7842

Ctrl + a and then

d # detach
p # switch to previous screen
n # switch to next screen
x # Lock screen
k # kill screen
```

### sed
```bash
# delete the string and create the backup of the file
sed -i.bak '/stringtodelete/d' file
# Add line after matching line.
sed -i '/\[Date\]/a date.timezone="Europe/Berlin"' /etc/php.ini
# replace " with blank in a file
sed -i -e 's/\"//g' test.json
# replace " with a blank on a output
grep -E 'ERROR|SFTP' test.json | cut -d',' -f2 | sed 's/\"//g'
# delete empty line
sed '/^\s*$/d'
# ??
cat /tmp/cacerts.pem | sed -n '/^pattern1/,/^pattern2/p;'
# From 3.10.0-862.11.6.el7.x86_64 extracts  and prints RHEL7
# \2 tells sed to print the value determined by second expression
uname -r | sed 's/\(.*\)el\([0-9]*\)\(.*\)/RHEL\2/'
```

### sftp
```bash
sftp user@server
?
# displays available commands
lcd
lls
lpwd, pw
put local-path [remote-path]
get remote-path [local-path]
```

### showmount
```bash
# Shows available shares on NFS server
showmount -e
```

### ssh
```bash
# Just if you want ssh to return fail status for a password prompt.
ssh -o NumberOfPasswordPrompts=0 servername
result=$?
if [ $result == "0" ]; then echo "success"; else echo "failed"; fi

# Send command and get output 
ssh -t $server "$COMMAND"

# connect to server and execute the script. 
ssh $server 'bash -s' &lt; script_to_execute.sh

# to avoid prompting for password.
# -o PasswordAuthentication=No this option seems not working. 
ssh -o PreferredAuthentications=publickey -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no servername
# ssh tunnel
ssh -p 22030 -L 22039:127.0.0.1:80 127.0.0.1 -N
```

### sshpass
```bash
ssh-copy-id -i id_rsa.pub user@servername

sshpass -p 'YourPassword' ssh-copy-id -i id_rsa.pub user@servername

sshpass -p 'YourPassword' ssh-copy-id -o "StrictHostKeyChecking no" -i id_rsa.pub user@servername
```

### subscription-manager
```bash
subscription-manager repos --enable &lt;&lt;REPO_NAME&gt;&gt;
subscription-manager repos --list
```

### tar
```bash
tar -cf compressed.tar /data/compressed # c - create, f - filename
tar -czf compressed.tar /data/compressed # z - compress files using gzip
tar -xzf compressed.tar # x - untar
tar -tvf compressed.tar # t - list the contents 
tar -xvf cleanfiles.sh.tar cleanfiles.sh
tar --extract --file=cleanfiles.sh.tar cleanfiles.sh # extract single file from .tar
tar -zxvf tecmintbackup.tar.gz tecmintbackup.xml # extract single file from .tar.gz 
tar -xvf tecmint-14-09-12.tar "file 1" "file 2" # extract multiple files.
tar -zxvf MyImages-14-09-12.tar.gz "file 1" "file 2" 
tar -jxvf Phpfiles-org.tar.bz2 "file 1" "file 2"
tar -xvf Phpfiles-org.tar --wildcards '*.php' # extract files with extensions
tar -zxvf Phpfiles-org.tar.gz --wildcards '*.php'
tar -jxvf Phpfiles-org.tar.bz2 --wildcards '*.php'
tar -rvf tecmint-14-09-12.tar xyz.txt # add files
tar -rvf tecmint-14-09-12.tar php
tar jcvf /user-backups/tecmint-home-directory-backup.tar.bz2 /home/tecmint # backup user data

# extract the files to a folder specified as --xform
tar -xf temp_files_20_04_2017.tar.gz --xform='s|^|myarchive/|S'

# TEST using Dry run "t"
tar -tf temp_csv_files_20_04_2017.tar.gz --xform='s|^|myarchive/|S' --verbose --show-transformed-names
```

### time
```bash
# for half million files
for i in $(seq 1 500000); do echo testing &gt;&gt; $i.txt; done

# takes too long for long list of files.
time rm -f *

# 14 Minutes for half a million files 
time find ./ -type f -exec rm {} \;

# 5 Minutes for half a million files 
time find ./ -type f -delete

# 1 Minute for half a million files 
time perl -e 'for(&lt;*&gt;){((stat)[9]&lt;(unlink))}'

# 2 Minute 56 seconds for half a million files 
time rsync -a --delete blanktest/ test/
```

### tmux
```bash
# http://www.hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/

tmux new -s new_name

# Display list of tmux sessions
tmux ls

# Attach the session
tmux attach -t 0

tmux rename-session -t 0 new_name

# Close a pan or detaching terminal session
Ctrl + d

Ctrl + b 

        % # new vertical split pane
        " # new horizontal split pane
        c # creates new window
        p # switch to previous window
        n # switch scto next window
        ←, ↑, →, ↓ # Navigate between panes
        &lt;number&gt; # switch to the window specified by the number.
        d # Detach from the current session
        , # rename window
        ? # See lit of commands
        Ctrl + Arrow Keys # Press the arrow keys continuously to resize the pane.
        # broadcast to all the panes
        :synchronize-panes on
        :synchronize-panes off
        # broadcast command
        setw synchronize-panes on
```

### top
```bash
# http://blog.scoutapp.com/articles/2015/02/24/understanding-linuxs-cpu-stats

top

top -p 34333

# display all the thread processes under this main proces
top -H -p 34333

# print top command output to console or give as input to other programs
top -bn 1

# Calculate cpu usage ??? This is sure not workng…
top -bn 1 | awk '{print $9}' | tail -n +8 | awk '{s+=$1} END {print s}'

# another way of calculating cpu usage
top -bn 3 | grep 'Cpu' | tail -n 1 | gawk '{print $2+$4+6}'
```

### touch
```bash
# creates a readme file with modified time as 2016-09-21 08:55:45
touch -t 201609210855.45 readme.txt
```

### tr
```bash
tr '\0' '\n' #cat /proc/1336/environ | tr '\0' '\n'
```

### tracking process
```bash
# gives the process id of the perticualr application use this with netstat
pgrep -f /FMBI/

# To see the connections opened on the given port
netstat -anp | grep 30000

netstat -ant

# display all the incoming and outgoing ports in action including the process id
netstat -tulpn

# display which program is responsible for the process 3813
ls -l /proc/3813/exe

# also using fuser command who is running on port 7000
fuser 7000/tcp =&gt; 3813

# current working directory of the process
ls -l /proc/3813/cwd
```

### trap
executes commands when some signals are received
```bash
trap -l # displays list of signals that can be captured by trap command
trap "rm $TEMP_FILE; exit" SIGHUP SIGINT SIGTERM # removes temp file if any of the signals are received
```

### unrar
```bash
unrar x -p$rarPassword "$rarFile" "$baseFile"
```

### useradd
```bash
useradd -g sales tom # Add a new user tom to sales group 
useradd -m -g sales tom # also creates a home directory
```

### userdel
```bash
userdel --remove techmint
```

### usermod
```bash
usermod -g sales jerry # add existing user jerry to sales group
usermod -G purchase jerry # add existing user jerry to secondary group purchase
```

### vim
```bash
:%s/foo/bar/g # replace globally with bar
:%s/foo/bar/gc # ask for confirmation
:%s/foo/bar/gci # case insensitive 
:%/foo/bar/gcI
:set number
:set nonumber
:noh 
:set list # display hidden characters
:set nolist # un hide the hidden characeters
:colorscheme # display the current color scheme
:color delek # set the current color scheme
:scriptnames # display the paths where vim is running and configs.
~/.vimrc # set default color
colo delek
Shift G # end of file - start of the line
gg # beginning of the file
$ # end of the line
0 or ^ # beginning of the line
i I , a A, o O # insert operations
u # undo
d # delete character
dw, d2w # delete the word
d$ # delete to the end of the line
dd, 2dd
:g/^\s*$/d # delete empty lines
:%s/ /\r/g # # replace spaces with new line
:g/.string.*/norm $x # search line and delete last character (which is comma here)
:g/check_enabled/d # search for the string and delete the complete line
:set fileformat=unix # set file format to unix
:set list # displays special characters
```

### w
```bash
# displays who logs in and system up time
w
```

### wget
```bash
wget http://download.virtualbox.org/virtualbox/5.0.20/
# specify headers parameter
wget -O/tmp/tmp —header=‘HostName: blog.test.com’ test.com
```

### ypcat
```bash
# print values of all keys in a NIS database
ypcat -k auto.projects
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

### yumdownloader
```bash
yumdownloader icinga2-ido-mysql-2.9.2-1.el7.icinga.x86_64
```

### zip
```bash
zip -er archive.zip /path/to/directory/       # zip folder with password
zip -e archivename.zip filetoprotect.txt      # zip single file with password
```