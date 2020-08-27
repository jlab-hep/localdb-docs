# Basic Tutorial

This tutorial explains:

1. [How to Setup YARR](#1-how-to-setup-yarr)
2. [How to Run Scan and Upload Results into Local DB](#2-how-to-run-scan-and-upload-results)
3. [How to Retrieve Data from Local DB](#3-how-to-retrieve-data)
4. [How to Setup Viewer Application](#4-how-to-setup-viewer)
5. [How to Check Data in Viewer Application](#5-how-to-check-data-in-viewer)

If you do not have [YARR git repository](https://gitlab.cern.ch/YARR/YARR) or [Local DB Tools git retpository](https://gitlab.cern.ch/YARR/localdb-tools), or system packages required for those repositories, see the [installation guide](installation.md) to install the missing ones.

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

#### Setup for DB-related functions

Next make sure to setup Local DB configuration files using [YARR/localdb/setup_db.sh](setup-db.md) script:

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

## 2. How to Run Scan and Upload Results

#### Run scan command

Scan and upload the results into Local DB using [YARR/bin/scanConsole -W](scanconsole.md) binary command:

```bash
$ ./bin/scanConsole \
-r configs/controller/emuCfg.json \
-c configs/connectivity/example_fei4b_setup.json \
-s configs/scans/fei4/std_digitalscan.json \
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

## 4. How to Setup Viewer

#### Setup configuration

Change the directory where you have cloned [Local DB Tools](https://gitlab.cern.ch/YARR/localdb-tools):

```bash
$ cd path/to/localdb-tools
```

And load path to ROOT installed directory to enable the plotting function in the viewer application:

```bash
$ source path/to/root/bin/thisroot.sh
```

First make sure to setup the configuration files of the [viewer application](viewer.md) using [localdb-tools/viewer/setup_viewer.sh](setup-viewer.md) script:

```bash
$ cd viewer
$ ./setup_viewer.sh
```

This script checks missing python packages, prepares default config files, install some useful functions using git.

```bash
### script output
Local DB Server IP address: 127.0.0.1
Local DB Server port: 27017

[LDB] Are you sure that's correct? [y/n]
> y
```

Answer **y** to proceed if you did not change any settings when you installed MongoDB.<br>

```bash
### script output
[LDB] Do you use admin functions for LocalDB viewer? [y/n]
> n
```

Answer **n** to proceed.

!!! Note
    Once you enable the administrator function, you can use various functions in the viewer application.<br>
    In this tutorial, you will skip that step and proceed next.<br>
    See [what can be done with the admin function and how to set it] to get more information.<br>

This script creates the [viewer config file](viewer-config.md).

#### Run application

Run python script to start the [viewer application](viewer.md) on the local host machine:

```bash
$ python3 app.py --config user_conf.yml
2020-08-27 15:28:09 guest0 root[29905] INFO [LDB] Viewer Application URL: http://127.0.0.1:5000/localdb/
 * Serving Flask app "app" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
2020-08-27 15:28:09 guest0 werkzeug[29905] INFO  * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

You can access the Local DB viewer on the local browser while this application is running.<br>

## 5. How to Check Data in Viewer

#### Top Page

Access [http://127.0.0.1:5000/localdb/](http://127.0.0.1:5000/localdb/) on the local browser:

|![Viewer Top Page](images/viewer_top.png)|
|:-:|

<br>

#### Scan List Page

Click **Scan Page** to switch to the scan list page:

|![Viewer Test Top Page](images/viewer_top_test.png)|
|:-:|

<br>

#### Scan Result Page

Click **result page** to switch the scan result page:

|![Viewer Result Page](images/viewer_result.png)|
|:-:|

<br>
