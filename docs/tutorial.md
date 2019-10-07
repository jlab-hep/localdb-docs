# Quick Tutorial

You can store result data by YARR immediately following the tutorial.

## 0. Installation

This step should be done by the administrator of the machine.<br>
The detail can be checked [Quick Installtion](#quick-installation).

## 1. Setup YARR command with Local DB

```bash
$ cd YARR
$ git checkout devel
$ mkdir build
$ cd build
$ cmake3 ../
$ make -j4
$ make install
$ cd ../
```

## 2. Setup Local DB Directory

- Set Local DB directory by `setup_db.sh`.

```bash
$ ./localdb/setup_db.sh
[LDB] Confirmation
<some texts>
[LDB] Continue? [y/n]
[LDB] > y
<some text>
[LDB] This description is saved as ${HOME}/YARR/localdb/README
```

- Confirme Local DB tools

```bash
$ ./localdb/bin/localdbtool-upload init
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# Local DB Server: mongodb://127.0.0.1:27017
#DB INFO# ---> connection is good.
#DB INFO# -----------------------
```

If there are some problems in the step, [FAQ](#faq) should be helpful for solving it.

## 3. scanConsole with Local DB

- scanConsole
   
You can scan and upload result data into Local DB by `scanConsole -W`

```bash
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

**Additional options**

- **-d ``<database config>``** : Set database config file (default: `${HOME}/.yarr/localdb/${HOSTNAME}_database.json`)
- **-u ``<user config>``** : Set user config file ([sample](#user-config-file))
- **-i ``<site config>``** : Set site config file ([sample](#site-config-file))

- Confirmation

There are three ways to confirm the data uploaded.

1. Log File
   
You can check if the upload is success in log file `${HOME}/.yarr/localdb/log/day.log`.

```log
2019-08-01 10:55:46,821 - INFO: -----------------------
2019-08-01 10:55:46,821 - INFO: Function: Upload Scan Data
2019-08-01 10:55:46,823 - INFO: Local DB Server: mongodb://127.0.0.1:27017
2019-08-01 10:55:46,826 - INFO: ---> connection is good.
2019-08-01 10:55:46,826 - INFO: Cache Directory: /home/akubata/work/YARR/data/000186_std_digitalscan/
2019-08-01 10:55:47,058 - INFO: Success
2019-08-01 10:55:47,060 - INFO: -----------------------
```

2. Retrieve Tool

You can check uploaded test log in CUI command `localdb/bin/localdbtool-retrieve`.

```bash
$ ./localdb/bin/localdbtool-retrieve log 
#DB INFO# -----------------------
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017
#DB INFO#    The connection is GOOD.
test data ID: 5d4c94c1fd212a639247b044 
User      : arisa_kubota at tokyo_institute_of_technology
Date      : 2019/08/08 14:31:39
Chip      : RD53A-001, RD53A-001_chip1
Run Number: 255
Test Type : std_analogscan
DCS Data  : NULL

test data ID: 5d4c89a4e34d9efb40565e65 
User      : arisa_kubota at tokyo_institute_of_technology
Date      : 2019/08/08 13:44:14
Chip      : RD53A-001, RD53A-001_chip1
Run Number: 251
# Ctrl+C can terminate the output test log
```

3. Viewer Application

You can check uploaded test data in GUI when Viewer Application is running. ([How to run the Viewer Application](#viewer-application))<br>
Access `http://127.0.0.1:5000/localdb/` or `http://IPaddress/localdb` in browser.


