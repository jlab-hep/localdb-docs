# Basic Tutorial

This tutorial describes the basic operations from scan to data upload after the [installation](installation.md).

!!! Warning
    If you do not have [YARR git repository](https://gitlab.cern.ch/YARR/YARR) or [Local DB Tools git retpository](https://gitlab.cern.ch/YARR/localdb-tools), or system packages required for those repositories, see the [installation guide](installation.md) to install the missing ones.

!!! Recommend
    If you could not install the requirements according to the [installation guide](installation.md) or cannot build YARR and cannot use read-out binary command, see the [trial tutorial](trial-tutorial.md) to try starting Local DB and using the commands.<br>
    Once you have started Local DB in [this trial tutorial](trial-tutorial.md), you can go to the [tutorial for the viewer application](viewer-tutorial.md) and use it.

### Table of Contents

1. [How to Setup YARR](#1-how-to-setup-yarr)
2. [How to Run Scan and Upload Results into Local DB](#2-how-to-run-scan-and-upload-results)
3. [How to Retrieve Data from Local DB](#3-how-to-retrieve-data)

---

## 1. How to Setup YARR

#### Setup for YARR binary command

First make sure to build YARR SW:

```bash
$ cd YARR
$ mkdir build && cd build

# for linux
$ cmake3 ../

# for macOS
$ cmake ../ -DCMAKE_TOOLCHAIN_FILE=../cmake/macos-clang

$ make -j4
$ make install
$ cd ../
```

#### Setup for Local DB configuration

Next setup Local DB configuration files using [YARR/localdb/setup_db.sh](setup-db.md) script:

```bash
$ ./localdb/setup_db.sh
```

This script checks missing python packages, prepares default config files, checks DB connection.

```bash
### script output
[LDB] -----------------------
[LDB] --  Mongo DB Server  --
[LDB] -----------------------
[LDB] IP address       : 127.0.0.1
[LDB] port             : 27017
[LDB] database name    : localdb
[LDB] -----------------------
[LDB] Are you sure that is correct? (Move to edit mode when answer 'n') [y/n/exit]
[LDB] > y
```

Answer **y** to proceed if you did not change any settings when you installed MongoDB.<br>
The script creates the [database config file](database-config.md).

```bash
### script output
[LDB] -----------------------
[LDB] --  User Information --
[LDB] -----------------------
[LDB] User Name        : username
[LDB] User Institution : localhost
[LDB] -----------------------
[LDB] Are you sure that is correct? (Move to edit mode when answer 'n') [y/n/exit]
[LDB] > n
```

Answer **n** and change the user config file to your name and institution name.<br>
The script creates the [user config file](user-config.md).


```bash
### script output
[LDB] -----------------------
[LDB] --  Site Information --
[LDB] -----------------------
[LDB] site name        : localhost
[LDB] -----------------------
[LDB]
[LDB] Are you sure that is correct? (Move to edit mode when answer 'n') [y/n/exit]
[LDB] > n
```

Answer **n** and change the site name to your institution name or where you are.<br>
The script creates the [site config file](site-config.md).

```bash
[LDB] Checking the connection...
[  info  ]: ------------------------------
[  info  ]: Function: Initialize upload function and check connection to Local DB
[  info  ]: -> Setting database config: /home/.yarr/localdb/localhost_database.json (default)
[  info  ]: Checking connection to DB Server: mongodb://127.0.0.1:27000/localdb ...
[  info  ]: ---> Good connection!
[  info  ]: ------------------------------
[LDB] Done.
...
```

The output of "Good connection!" means that the connection to Local DB can be confirmed.

## 2. How to Run Scan and Upload Results

#### Run scan command

You can upload results into Local DB after [YARR/bin/scanConsole](scanconsole.md) just by adding option '-W':

```bash
### FEI4B emulator
$ ./bin/scanConsole \
-c configs/connectivity/example_fei4b_setup.json \
-r configs/controller/emuCfg.json \
-s configs/scans/fei4/std_digitalscan.json \
-W

### RD53A emulator
$ ./bin/scanConsole \
-c configs/connectivity/example_rd53a_setup.json \
-r configs/controller/emuCfg_rd53a.json \
-s configs/scans/rd53a/std_digitalscan.json \
-W

<lots of text>
[  info  ]: Succeeded uploading scan data from /home/work/YARR/data/000004_std_digitalscan
```

The output of "Succeeded uploading" means that data was uploaded into Local DB successfully.

#### Check log

You can check if the upload is success in log file `HOME/.yarr/localdb/log/log`:

```bash
$ cat /home/.yarr/localdb/log/log
[  info  ]: -----------------------
[  info  ]: Function: Upload scan data from specified directory
[  info  ]: Cache Directory: /home/work/YARR/data/000004_std_digitalscan
...
[  info  ]: Succeeded uploading scan data from /home/work/YARR/data/000004_std_digitalscan
[  info  ]: -----------------------
```

## 3. How to Retrieve Data

#### Data Log

Check the uploaded scan data using [YARR/bin/dbAccessor -L](accessor.md) binary command:

```bash
$ ./bin/dbAccessor -L
[  info  ]: DBHandler: Retrieve Test Log
[  info  ]: -----------------------
test data ID: 5f4743b09231c6b44ba0ef38
User      : username at institution
Date      : 2020/08/27 14:03:51
Component : JohnDoe_0
Run Number: 4
Test Type : std_digitalscan
DCS Data  : NULL
### Ctrl+C can terminate the output test log
```

#### Data Donwload

Retrieve the scan data using [YARR/bin/dbAccessor -D](accessor.md) binary command:

```bash
$ ./bin/dbAccessor -D
[  info  ]: DBHandler: Retrieve Config Files
[  info  ]: -----------------------
[  info  ]: Retrieve ... ./db-data/ctrlCfg.json
[  info  ]: Retrieve ... ./db-data/dbCfg.json
[  info  ]: Retrieve ... ./db-data/siteCfg.json
[  info  ]: Retrieve ... ./db-data/userCfg.json
[  info  ]: Retrieve ... ./db-data/std_digitalscan.json
[  info  ]: Retrieve ... ./db-data/JohnDoe_0_EnMask.json
[  info  ]: Retrieve ... ./db-data/JohnDoe_0_OccupancyMap.json
[  info  ]: Retrieve ... ./db-data/fei4b_test.json
[  info  ]: Retrieve ... ./db-data/fei4b_test.json.before
[  info  ]: Retrieve ... ./db-data/fei4b_test.json.after
[  info  ]: Retrieve ... ./db-data/connectivity.json
[  info  ]: Retrieve ... ./db-data/scanLog.json
[  info  ]: -----------------------
```

* List of restored data (default dir: `./db_data`)
    * Test Information (Data ID, User, Date, Chips, Run #, Test type)
    * config files ([connectivity](connectivity-config.md), controller, scan, [chip](chip-config.md), [database](database-config.md), [user](user-config.md), [site](site-config.md))
    * result data file

---

Go to the [tutorial for the viewer application](viewer-tutorial.md) to check the data stored in the Local DB and the uploaded scan data in the browser.<br>
Go to the [advanced tutorial](advanced-tutorial.md) to get a more advanced usage.
