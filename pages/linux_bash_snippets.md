---
layout: page
title: Bash Snippets
categories: [linux]
tags: [bash, shell-scripting]
type: page
---


### Get command line parameters using $#
```bash
if [[ $# -eq 2 ]]; then
    echo ""
fi
```
### for loop
```bash
for f in *.tar*;  do 
    
done
```
### Format output using printf
```bash
printf "\n %-10s %8s %10s %11s\n" "ITEM NAME" "ITEM ID" "COLOR" "PRICE"
format=" %-10s %08d %10s %11.2f\n"
printf "$format" \
Triangle 13  red 20 \
Oval 204449 "dark blue" 65.656 \
Square 3145 orange .7
```
### Check if file or directory exists
```bash
if [ -f ~/.bashrc ]; then
    echo "file exists";
fi
if [ -d ~/.ssh ]; then
    echo "Directory exists";
fi
```
### Know which shell you are working on
```bash
echo $0
echo $SHELL
```
### Formatted output using printf
```bash
format="%28s %-7s %40s %15s"
printf "$format" "file transfered to server - " "success" " - $FILE_TO_TRANSFER" "- $server:/tmp" >> output.log
```
### Creating array from the string
```bash
str="autoconf has no dependents. automake has no dependents."
IFS=.
ary=($str_list)
for key in "${!ary[@]}"; do 
    echo "$key ${ary[$key]}";
done
```

```bash
IFS=$'\n'
serverList=$( cut -d',' -f1 server_list.txt | uniq -i)
read -rd '' -a servers <<< "$serverList"
for server in "${!servers[@]}"
do
    result=$(ssh -t $server 'uptime')
    echo "$server uptime is $result"
done
```
### Loop through an array

```bash
launchctlFind () {
    LaunchctlPATHS=( \
        ~/Library/LaunchAgents \
        /Library/LaunchAgents \
        /Library/LaunchDaemons \
        /System/Library/LaunchAgents \
        /System/Library/LaunchDaemons \
    )

    for curPATH in "${LaunchctlPATHS[@]}"
    do
        grep -r "$curPATH" -e "$1"
    done
    return 0;
}
```

### Round float values
```bash
# Round Float value to floor 99.8 -> 100
CPU_USAGE=99.8
CPU_USAGE_INT=$( printf "%.0f" $CPU_USAGE )
# Round Float value to ceil 99.8 -> 99
CPU_USAGE=99.8
CPU_USAGE_INT=`echo $CPU_USAGE | awk '{print int($0)}'`
```
### Execute command using character `
```bash
CPU_USAGE_INT=`echo $CPU_USAGE | awk '{print int($0)}'`
```
### Get file name and extension
```bash
fileExtension="${fullFileName##*.}"
 fileName="${fullFileName%.*}"
```
### Loop through tar files and create a folder with the name
```bash
for f in *.tar*;  do 
    fileName=$(basename $f); 
    dirName=${fileName:0:${#fileName} - 7}; 
    mkdir $dirName; 
    tar -xvzf $f -c $dirName; 
done
```
### Loop through the content of a file
```bash
while read LINE
do
    echo "$LINE"
done < file.txt
```

```bash
IFS=$'\n'
set -f     # Disable globbing
for LINE in $(cat < "$1"); do
      echo "$LINE"
done
```
### Check if grep returns some result or not
```bash
if ! grep -q ".bashrc" ~/.bash_profile ; then
    echo "adding .bashrc to .bash_profile"
    echo ". ~/.bashrc" >> ~/.bash_profile;
    source ~/.bash_profile;
else
    echo "** .bashrc already exists in .bash_profile"
fi
```

```bash
TEST=$(ps -ef | grep crond)
 
if [ "$TEST" != "" ]
then
    echo "crond is already running"
else
    echo "starting crond"
    /usr/bin/crond
fi
```
### Trim String
```bash
function trim()
{
    str="$1"
    result=$(echo $str | sed 's/^ *//g')
    result=$(echo $result | sed 's/ *$//g')
    echo $result
}
```
### Print all folders and subfolders and file count
```bash
find . -type d -print0 | sort -z | while read -d '' -r dir; do
    files=("$dir"/*);
    printf "%5d files in directory %s\n" "${#files[@]}" "$dir";
done
```
### Display file names with spaces
```bash
find . -type f -name "*.csv" -print0 | while IFS= read -r -d '' file; do
    echo "file = $file"
done

OIFS="$IFS"
IFS=$'\n'
for file in `find . -type f -name "*.csv"`  
do
     echo "file = $file"
done
IFS="$OIFS"
```
### Find Songs With Lyrics
```bash
find . -type f -iname "*.mp3" -print0 | while IFS= read -r -d '' file; do 
    lyrics=$(exiftool -TAG "-Lyrics" "$file"); 
    if [[ ${#lyrics} -gt 300 ]]; then 
         echo "$file---->${#lyrics}----> YES"; 
    fi  
done
```
### Use awk to count sum of files in folders
```bash
for d in $(find . -type d ); do 
    if [ "$(ls $d)" ]; then 
        echo "$d > $(ls -l $d | wc -l)"; 
    fi 
done | awk -F'>' '{ gsub(/ /,"",$2); sum += $2; if($2>100) printf "%-120s -> %-4s -> %-6s\n", $1, $2, sum}'
```
### Find empty directories
```bash
for d in $(find . -type d); 
do
         if [ -z "$(find $d -type f)" ]; then 
                    echo "$d is empty"; 
         fi
done
```
### Increment counter inside while loop
Note that the counter here is still zero.

```bash
counter=0
find ~/scripts/python/2_photos/ -type f -iname "$1" | while read -r file; do
      counter=$((count+1))
done
echo "counter - $counter"
```

This is the correct approach for the counter to hold its incremented value after the loop.

```bash
counter=0
while read -r file; do
      counter=$((count+1))
done < <(find ~/scripts/python/2_photos/ -type f -iname "$1")
echo "counter - $counter"
```
### Print bulk formatted string output using ‘Bash Here Documents’
```bash
function printHelp()
{
   cat <<EOT
   
   ---Description---
   This is about using cat wisely
 
   --Usage--
   test <params>
   
   EOT
}
```

```bash
cat << EOF > /drive/file.txt
The content you want to write here
which could be a multi line
EOF
```

```bash
# In order to disable interpreting variables use single quotes
 cat >> 'EOF' > /drives/file.txt
Disable vairable interpretation $VAR
EOF
```

```bash
# Use <<- (followed by a dash) to disable leading tabs in a script
# This is mainly useful when you use indentation in the script
# Below example, cat is started with a tab. So use <<-
 
while true; do
   cat <<- EOF > /drives/file.txt
   Enter all the files you want
   here
   EOF
done
```
### Get File path / basename
```bash
FILE=/User/Documents/testing.tar.gz
FILE_PATH=${FILE%/*} 
FILE_BASE=${FILE##*/}
FILE_PREFIX=${FILE_BASE%.*} 
FILE_EXT=${FILE_BASE##*.}
```
### Get first few characters of a string
```bash
FILE_NAME=" file_name_with_first_space.mp3"
FIRST_CHAR="${FILE_NAME:0:1}"
if [[ $FIRST_CHAR == " " ]]; then      
      echo "FILE first char is space"; 
fi
```

Removing First Empty Space In File Names

```bash
while read -r file; do 
  FILE_NAME=${file##*/}; 
  FIRST_CHAR="${FILE_NAME:0:1}"; 
  if [[ $FIRST_CHAR == " " ]]; then 
    # trim file name
    result="$(echo $FILE_NAME | sed 's/^ *//g')";  
    result=$(echo $result | sed 's/ *$//g'); 
     echo "Renaming FILE >$FILE_NAME< TO >$result<"; 
    mv "$FILE_NAME" "$result";  fi 
done < <(find . -type f)
```
### Extract content between two specific lines
Extract content between two specific lines and give it as input to another command
```bash
BEGIN_LINE="-----BEGIN CERTIFICATE-----"
END_LINE="-----BEGIN CERTIFICATE-----"
EXTRACTED_CONTENT=""
READ="false"
PRINT="false"
READ_BEGIN_END="true"
while read LINE; do	
	if [ "$END_LINE" = "$LINE" ]; then
		READ="false"
		PRINT="true"
	fi
	
	if [ "$READ" == "true" ]; then
		EXTRACTED_CONTENT="$EXTRACTED_CONTENT$LINE\n"
	fi 
	 
	if [ "$PRINT" == "true" ]; then
		if [ "$READ_BEGIN_END" == "true" ]; then
			BEGIN_CONTENT="$BEGIN_LINE\n"
			END_CONTENT="$BEGIN_LINE\n"
			EXTRACTED_CONTENT="$BEGIN_CONTENT$EXTRACTED_CONTENT$END_CONTENT"
		fi
		printf %*s $COLUMNS | tr ' ' '-'
		printf -- "$EXTRACTED_CONTENT" | openssl x509 -noout -text
		printf -- "$EXTRACTED_CONTENT" | openssl x509 -noout -sha1 -fingerprint
		EXTRACTED_CONTENT=""
		PRINT="false"
	fi 
	
	if [ "$BEGIN_LINE" = "$LINE" ]; then 
		READ="true"
	fi 
 
done < /tmp/all_public_certs.pem
```
### If String contains
```bash
str=testing
substr=test
if [ "${str/$substr}" = "$str" ] ; then
  echo "${substr} is not in ${str}"
else
  echo "${substr} was found in ${str}"
fi
 
string='testing'
if [[ $string == *"test"* ]]; then
  echo "It's there!"
fi
```

### loop through grep result

```bash
grep xyz abc.txt | while read -r line ; do
    echo "Processing $line"
    # your code goes here
done
```

>The -r option to read prevents backslash interpretation (usually used as a backslash newline pair, to continue over multiple lines or to escape the delimiters). Without this option, any unescaped backslashes in the input will be discarded. You should almost always use the -r option with read.

>In the scenario above IFS= prevents trimming of leading and trailing whitespace. Remove it if you want this effect.

* http://mywiki.wooledge.org/BashFAQ/001

```bash
while read -r line ; do
    echo "Processing $line"
    # your code goes here
done < <(grep xyz abc.txt)
```

