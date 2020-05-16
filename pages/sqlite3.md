---
layout: page
title: Sqlite3
categories: [databases]
tags: [sqlite3, databases]
type: page
---


## Commands

```sql
.help

.import

# write result to a separate file
.mode list
.separator |
.output test_file_1.txt
select * from tbl1;
.exit

.schema tb1

#csv import
.mode csv
.import /work/somedata.csv tab1

#csv export
.header on
.mode csv
.once c:/work/dataout.csv
SELECT * FROM tab1;
.system c:/work/dataout.csv

# export to excel
.excel
SELECT * FROM tab;

# Converting An Entire Database To An ASCII Text File
sqlite3 ex1 .dump | gzip -c >ex1.dump.gz
zcat ex1.dump.gz | sqlite3 ex2
```

