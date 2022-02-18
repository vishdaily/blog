---
layout: page
title: Python
categories: [progamming-languagues]
tags: [programming-languagues, python]
type: page
---

# Links
[https://realpython.com/]

# Python tips

## sample python program
```python
def main(argv):
    print("hello")

if __name__ == "__main__":
    main(sys.argv[1:])
```

## interactive shell help
Use help() and dir() in python interactive shell to list class and method docs

```python
import pandas as pd
# list class doc
help(pd)
# list class methods
dir(pd)
# list class method usage and doc
dir(pd.read_csv)
```

## argparser
[https://mkaz.blog/code/python-argparse-cookbook/]

```python
import argparse
arser = argparse.ArgumentParser()
# action="store_true" or action="store"
parser.add_argument("-f", "--function" help="set output width", action="store", dest="function_name", default=???, type=??)
parser.add_argument('count', action="store", type=int)
```

# Use pyenv to work with python

Easient way to work with different python versions is using pyenv and pyenv-virtualenv
Firslty pyenv and pyenv-virutalenv modules needs to be installed 

## Install pyenv
[https://github.com/pyenv/pyenv]
## install pyenv-virtualenv

Note:: installing pyenv will also install pyenv-virtualenv
If you have installed pyenv, check if virtual-env is already installed in 
this path ```$(pyenv root)/plugins/pyenv-virtualenv```

add the following line in bashrc 
```bash

echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bash_profile
```
[https://github.com/pyenv/pyenv-virtualenv]

Alternatively check https://realpython.com/intro-to-pyenv/ for installation

### Common build errors

https://stackoverflow.com/questions/52873193/error-the-python-ssl-extension-was-not-compiled-missing-the-openssl-lib-inst

```bash
On Debian stretch (and Ubuntu bionic), libssl-dev is OpenSSL 1.1.x, but support for that was only added in Python 2.7.13, 3.5.3 and 3.6.0. To install earlier versions, you need to replace libssl-dev with libssl1.0-dev. This is being tracked in https://github.com/pyenv/pyenv/issues/945.

So if you don't need a specific version of 2.7 you can go ahead and install 2.7.13 and the error will not appear
```

## FAQ Commands
```bash
pyenv install --list | grep " 3\.[678]"
pyenv install --list | grep "jython"
pyenv install -v 3.7.2

# ls ~/.pyenv/versions/
pyenv uninstall 2.7.15

pyenv versions

which python
pyenv which python

# If, for example, you wanted to use version 2.7.15, then you can use the global command
pyenv global 2.7.15

# If you ever want to go back to the system version of Python as the default, you can run this:
pyenv global system

pyenv commands

# The local command is often used to set an application-specific Python version
pyenv local 2.7.15

# The shell command is used to set a shell-specific Python version
pyenv shell 3.8-dev
```

```bash
pyenv virtualenv <python_version> <environment_name>

pyenv virtualenv 3.6.8 myproject

# Activating Your Versions
pyenv local myproject

pyenv deactivate
```

## Running the script via crontab using pyenv

[http://blog.rubypdf.com/2018/10/12/how-to-set-virtualenv-for-a-crontab/]

cat << EOF >> /root/docker_data/scripts/nsedatadownloader/runpy
#!/bin/bash    
source /root/.pyenv/versions/3.5.4/envs/3_5_4/bin/activate

#virtualenv is now active, which means your PATH has been modified.
#Don't try to run python from /usr/bin/python, just run "python" and
#let the PATH figure out which version to run (based on what your
#virtualenv has configured).

python "$@"

#another way
#echo 'source /Users/steven/.pyenv/versions/3.6.4/envs/ts/bin/activate; python /Users/steven/tmp/hello.py' | /bin/bash
EOF


# Pandas

[https://honingds.com/blog/pandas-read_csv/]
## fequently used pandas commands
```python
import pandas as pd
filepath = 'test.csv'
pd_data = pd.read_csv(filepath)
list(pd_data.columns)
df  = pd.read_csv(file, usecols = ["SYMBOL \n", "PREV. CLOSE \n"])
df = pd.read_csv("f500.csv", usecols = lambda column : column not in ["company" , "rank", "revenues"])
pd.read_csv(filepath, skiprows=50, nrows=5)
# set data type for the csv column. use thousands=, if the float value has thousand separator
df = pd.read_csv(filepath, dtype = {"PREV. CLOSE \n" : "float64"}, thousands=',')
df.info()
# https://www.interviewqs.com/ddi_code_snippets/get_list_pandas_dataframe
```

## Looping through csv and fetching values
```python
for i, row in input_file_pd_data_n_rows.iterrows():
    symbol = row['SYMBOL']
    analyse_file_pd_data = pd.read_csv(str(path_in_str))
    analyse_file_row = analyse_file_pd_data.loc[analyse_file_pd_data['SYMBOL'] == symbol ]
    analyse_file_ltp = analyse_file_row['LATEST']
    analyse_file_ltp_value = analyse_file_ltp.iloc[0]
```

## Create dataframe and print in tabular format
```python
data = { 'Col1' : [val1, val2], 
'Col2' : [val3, val4] }
df = pd.DataFrame(data, columns = ['Col2', 'Col1']
print(df)
```


# Just few tips

## sort files based on timestamp
```bash
files = list(filter(os.path.isfile, glob.glob(args.dir_path + "/" + args.file_prefix + '*.csv')))
files.sort(key=lambda x: os.path.getmtime(x))
```

