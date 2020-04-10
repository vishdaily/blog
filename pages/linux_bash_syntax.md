---
layout: page
title: Bash Syntax
categories: [linux]
tags: [bash, shell-scripting]
type: page
---

### while loop
```bash
while true
do
    echo ""
done
```

### for loop
```bash
for f in *.tar*;  do 
    
done
```

### if elif else syntax
```bash
if [ "$test" == "--help" ]
then
    echo "1"
elif [ "$test" == "add" ]
then
    echo "add"
else
    echo "exit"
fi
```

### Format date
```bash
thread_dump_time=$(date +"%Y-%m-%d %H:%M:%S")
```

### Division
```bash
ACTUAL_CPU_USAGE=$((CPU_USAGE_INT / NO_OF_CPU_CORES))
```

### Arithmatic Operations
```bash
var=$((var+1))
```