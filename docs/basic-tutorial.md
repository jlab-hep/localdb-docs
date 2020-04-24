# Basic Tutorial

You can store result data by YARR immediately following the tutorial.

1. [Setup](#1-setup)
2. [Scan and Upload data into Local DB](#2-upload)
3. [Retrieve data from Local DB](#3-retrieve)

## 1. Setup

First please be sure to build YARR SW. <br>

```bash
$ cd YARR
$ mkdir build && cd build

# for linux
$ cmake3 ../

# for macOS
$ cmake ../ -DCMAKE_TOOLCHAIN_FILE=../cmake/macos-clang

$ make -j4
$ make install
```
> More detail about YARR SW: [YARR Docs](https://yarr.readthedocs.io/en/latest/)

And please be sure to setup Local DB setting using `setup_db.sh`. <br>
This script confirms if the python packages is satisfied, the default config files are prepared, the commands are enabled, and the DB connection is established. <br>

```bash
$ cd YARR
$ ./localdb/setup_db.sh
```
> More detail about setup_db.sh: [setup-db.sh command](setup-db.md)-->

## 2. Upload

You can scan and upload the test data into Local DB by `scanConsole -W` after [setup Local DB](#setup).

```bash
$ cd YARR
$ ./bin/scanConsole \
-r configs/controller/emuCfg.json \
-c configs/connectivity/example_fei4b_setup.json \
-s configs/scans/fei4/std_digitalscan.json \
-W
<lots of text>
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# Local DB Server: mongodb://127.0.0.1:27017
#DB INFO# ---> connection is good.
#DB INFO# -----------------------
#DB INFO# Uploading in the back ground. (log: ~/.yarr/localdb/log/)
```
> [More detail about scanConsole -W](scanconsole.md)

You can check if the upload is success in log file `HOME/.yarr/localdb/log/day.log`:

```log
2019-08-01 10:55:46,821 - INFO: -----------------------
2019-08-01 10:55:46,821 - INFO: Function: Upload Scan Data
2019-08-01 10:55:46,823 - INFO: Local DB Server: mongodb://127.0.0.1:27017
2019-08-01 10:55:46,826 - INFO: ---> connection is good.
2019-08-01 10:55:46,826 - INFO: Cache Directory: /home/akubata/work/YARR/data/000186_std_digitalscan/
2019-08-01 10:55:47,058 - INFO: Success
2019-08-01 10:55:47,060 - INFO: -----------------------
```

## 3. Retrieve

You can retrieve data from Local DB by `localdbtool-retrieve` after [setup Local DB](#setup).

- data log

You can check the uploaded test data log by `localdbtool-retrieve log`:

```bash
$ cd YARR
$ ./localdb/bin/localdbtool-retrieve log
#DB INFO# -----------------------
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017
#DB INFO#    The connection is GOOD.
test data ID: 5d8da5eda45ae057dbd1fbd6
User      : user at site
Date      : 2019/09/27 15:02:17
Chip      : JohnDoe_0
Run Number: 5635
Test Type : std_digitalscan
DCS Data  : NULL
# Ctrl+C can terminate the output test log
```
> [More detail about Retrieve Tool](retrieve.md)

- data download

You can retrieve the uploaded data into the local directory by `localdbtool-retrieve pull`:

**This function is not available in YARR v1.1.0.**<br>
**Please change to the devel branch if want to use.**<br>

```bash
$ cd YARR
$ ./localdb/bin/localdbtool-retrieve pull
#DB INFO# -----------------------
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017
#DB INFO#    The connection is GOOD.
#DB INFO# test data ID: 5d8da5eda45ae057dbd1fbd6
#DB INFO# - User      : user at site
#DB INFO# - Date      : 2019/09/27 15:02:17
#DB INFO# - Chips     : JohnDoe_0
#DB INFO# - Run Number: 5635
#DB INFO# - Test Type : std_digitalscan
#DB INFO# Retrieve ...
<some texts>
#DB INFO# -----------------------
```
> [More detail about Retrieve Tool](retrieve.md)

* List of restored data (default dir: `./db_data`)
    * Test Information (Data ID, User, Date, Chips, Run #, Test type)
    * connectivity config file
    * controller config file
    * scan config file
    * chip config file (original/before/after)
    * result data file
    * database config file
    * user config file
    * site config file
