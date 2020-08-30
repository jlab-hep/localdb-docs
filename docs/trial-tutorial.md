# Trial Tutorial

Assuming you do not have root privileges and can not complete the [installation of the requirements](installation.md), this tutorial describes how to build an environment in your user directory, setup a database with a sample dataset, and try it out.

!!! Warning
    This is just a tutorial to check the functions of Local DB, not the official method of setting it up.<br>
    When using the Local DB during productions, start it up according the [installation guide](installation.md).

!!! Recommend
    If you have already installed the requirements according to the [installation guide](installation.md), it is recommended to see the [basic tutorial](basic-tutorial.md) to get a more hands-on tutorial.<br>
    If you could not install or cannot build YARR and cannot use read-out binary command, proceed [this trial tutorial](trial-tutorial.md) to try starting Local DB and using the commands.<br>
    Once you have started Local DB in [this trial tutorial](trial-tutorial.md), you can go to the [tutorial for the viewer application](viewer-tutorial.md) and use it.

### Table of Contents

1. [How to Build Environment in User Directory](#1-how-to-build-environment)
2. [How to Use Read-out Command and Data Upload](#2-how-to-read-out-and-data-upload)

---

## 1. How to Build Environment

#### Clone git repository for this tutorial

First clone [localdb-dataset git repository](https://gitlab.cern.ch/akubota/localdb-dataset) just for this tutorial:

```bash
$ git clone https://gitlab.cern.ch/akubota/localdb-dataset.git
```

!!! Note
    It is required your account in gitlab.cern.ch to clone this repository.

#### Download MongoDB

Next download MongoDB packages using **localdb-dataset/install_mongo.sh**:

```bash
$ cd localdb-dataset
$ ./install_mongo.sh
[LDB] Select your OS from the list. (Type a-d from the list)

OS supported by tutorial
  a) RHEL 6.2 Linux x64
  b) RHEL 7.0 Linux x64
  c) macOS x64
OS not supported by tutorial
  d) Others

[LDB] > a
```

!!! Warning
    If your host machine is centOS7 or macOS, you can download MongoDB packages with this script, but other OS is not supported, so see the [MongoDB Community Server](https://www.mongodb.com/download-center/community) to install it.<br>
    Probably the tutorial doesn't work, sorry.

```bash
### script output
[LDB] Done.
[LDB] Check README to get how to use commands in ./mongodb-4.2.6/bin

[LDB] To make a path to commands in ./mongodb-4.2.6/bin you have to excute:
      $ export PATH=/root/work/localdb-dataset/mongodb-4.2.6/bin:$PATH

$ export PATH=path/to/mongodb-4.2.6/bin:$PATH
```

Once add the bin directory to the PATH, you can use MongoDB command frequently.

#### Download minimum sample dataset

Next download a minimized sample dataset of Local DB just for this tutorial using **localdb-dataset/download_minimumdb.sh**:

```bash
$ ./download_minimumdb.sh
...
[LDB] Done.
```

#### Start MongoDB Server

Next start MongoDB server with the provided config file just for this tutorial in **localdb-dataset/mongodb.conf**:

```bash
$ pwd
path/to/localdb-dataset

$ mongod --config mongod.conf &
$ cat mongod.conf | grep port
27000
```

The default port number for Local DB is **27017**, but in this tutorial, it is set to **27000** to avoid conflict.

```bash
$ mongo --port 27000 # Specify port number to MongoDB server
MongoDB shell version v4.2.6
> show dbs
admin    0.000GB
config   0.000GB
local    0.000GB
localdb  0.134GB
> exit
bye
```

You can check **localdb** if MongoDB is built with sample dataset.

## 2. How to Read-out and Data Upload

#### Setup for YARR binary command

First clone [YARR git repository](https://gitlab.cern.ch/YARR/YARR) and try to build YARR binary command:

```bash
$ git clone https://gitlab.cern.ch/YARR/YARR.git
$ cd YARR
$ mkdir build && cd build
$ cmake3 ../
$ make -j4
$ make install
$ cd ../
```

Even if this build fails due to environmental issues, this tutorial prepares a toy command of the [scanConsole](scanconsole.md), so you can use the command to try from read-out to data upload.<br>

#### Setup for Local DB confuguration

Next setup Local DB configuration files using [YARR/localdb/setup_db.sh](setup-db.md)

```bash
$ ./localdb/setup_db.sh -p 27000
```

This script checks missing python packages, prepares default config files, checks DB connection.

```bash
### script output
[LDB] -----------------------
[LDB] --  Mongo DB Server  --
[LDB] -----------------------
[LDB] IP address       : 127.0.0.1
[LDB] port             : 27000
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
### script output
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

#### Read-out and Upload

##### i. Upload w/ scanConsole (If you could compile YARR commands)

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

##### ii. Upload w/o scanConsole (If you could not compile YARR commands)

You can just generate scan-like results under data/last_scan using a script **localdb-dataset/scanConsole.sh**:

```bash
$ mv path/to/localdb-dataset/scanConsole.sh path/to/YARR/
$ cd path/to/YARR

### FEI4B digital scan
$ ./scanConsole.sh \
-c configs/connectivity/example_fei4b_setup.json \
-s digitalscan \
-W

### RD53A digital scan
$ ./bin/scanConsole.sh \
-c configs/connectivity/example_rd53a_setup.json \
-s digitalscan \
-W

<lots of texts>
[  info  ]: Succeeded uploading scan data from /home/work/YARR/data/000004_std_digitalscan
```

---

Go to the [tutorial for the viewer application](viewer-tutorial.md) to check the data stored in the Local DB and the uploaded scan data in the browser.<br>
Go to the [basic tutorial](basic-tutorial.md) to get a more hands-on tutorial.
