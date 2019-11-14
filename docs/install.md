This page describes how to setup Local DB Tools.<br>

- [OS supported by the Docs](#os)
- [List of Local DB Tools](#tools-list)
- [Pre Requirements](#pre-requirements)
- [Setup](#set-up)
    - [YARR/localdb](#yarrlocaldb)
    - [Local DB Tools](#local-db-tools)

## OS

This page supports:

* centOS7

## Tools Lost

There are several tools for handling Local DB.

* **Uploader** ([YARR/localdbtool-upload](#yarrlocaldb))<br>
    To upload data (test data, chip data, user data, site data ...) into Local DB.

* **Retriever** ([YARR/localdbtool-retrieve](#yarrlocaldb))<br>
    To retrieve data (data log, data files) from Local DB.

* **Handler** ([YARR/bin/dbAccessor](#yarrlocaldb)) <br>
    To handle (upload/register/retrieve) data in Local DB.

* **Viewer Application** ([localdb-tools/viewer](#local-db-tools))<br>
    To check/edit data in Local DB on browser.

* **Synchronization Tool** ([localdb-tools/sync-tool](#local-db-tools))<br>
    To push/pull/share data with the other Local DB or Master Server (Centralize Local DB).

* **Archive Tool** ([localdb-tools/archive-tool](#local-db-tools))<br>
    To create archive tar.gz file for Local DB back-up.

## Pre Requirements

#### YARR System ( [git](https://gitlab.cern.ch/YARR/YARR) )

Ensure that [YARR SW](https://yarr.readthedocs.io/en/latest/install/) is installed and set-up. <br>
**Use devel branch for trying the latest functions.**<br>
Check `scanConsole`, which is the main read-out program, working by:

```bash
$ cd <YARR SW installation dir>
$ bin/scanConsole -r configs/controller/emuCfg.json -c configs/connectivity/example_fei4b_setup.json -s configs/scans/fei4/std_digitalscan.json -p
```

This runs a digitalscan with the FE-I4B emulator.<br>
This does not use or require any hardware and will run purely in software.

#### Local DB System: MongoDB

Ensure that [MongoDB](https://localdb-docs.readthedocs.io/en/devel/requirements/#mongo-db) is installed and started. <br>
Check `mongo`, which is the command to access MongoDB, working by:

```bash
$ mongo [--port <port number>]
MongoDB shell version v4.2.1
...
> db
test
> exit
bye
```

#### Local DB Tools ( [git](https://gitlab.cern.ch/YARR/localdb-tools) )

Ensure that [Local DB Tools](https://localdb-docs.readthedocs.io/en/devel/requirements/) is installed and set-up. <br>
**Use devel branch for trying the latest functions.**

#### Required packages (yum, python)

Check [Pre Requirements](https://localdb-docs.readthedocs.io/en/devel/requirements/) to install required packages.

## Settings

### YARR/localdb

There are three Local DB tools included in YARR SW:

* Uploader (localdbtool-upload)
* Retriever (localdbtool-retrieve)
* Handler (dbAccessor)

#### 1. Set-up Local DB Tools in YARR

`YARR/localdb/setup_db.sh` can set-up Local DB Tools in user local environments by following steps:

* Create the user directory for Local DB ---> ${HOME}/.yarr/localdb
* Create the database config file ---> [${HOME}/.yarr/localdb/${HOSTNAME}_database.json](config.md)
* Check if required python modules are installed

```bash
$ cd <YARR SW installation dir>
$ ./localdb/setup_db.sh
[LDB] Confirmation
[LDB] -----------------------
[LDB] --  Mongo DB Server  --
[LDB] -----------------------
[LDB] IP address      : 127.0.0.1
[LDB] port            : 27017
[LDB] database name   : localdb
[LDB]
[LDB] Are you sure that is correct? [y/n]
[LDB] > y
[LDB]
[LDB] This script performs ...
[LDB]
[LDB]  - Check pip packages: '<YARR SW installation dir>/localdb/setting/requirements-pip.txt'
[LDB]  - Create Local DB files: '${HOME}/.yarr/localdb/obsidian_database.json'
[LDB]
[LDB] Continue? [y/n]
[LDB] > y

< Setting up with some texts >

[LDB] More detail:
[LDB]   Access 'https://localdb-docs.readthedocs.io/en/master/'
```

**Additional options**

- **-i ``<IP address>``** : Set Local DB server IP address (default: 127.0.0.1)
- **-p ``<port>``** : Set Local DB server port (default: 27017)
- **-n ``<DB name>``** : Set Local DB Name (default: localdb)
- **-a ``<CA file>``** : Path to CA certificate of Local DB server (option)
- **-e ``<Certification>``** : Path to Client certificate of Local DB server (option)
- **-r** : Clean the settings (reset)

#### 2. Confirmation

Please run the command with the option 'init' to check if the command is working or the connection to Local DB is good.

```bash
$./localdb/bin/localdbtool-upload init
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017/localdb
#DB INFO# ---> Connection is GOOD.
#DB INFO# -----------------------
$
$./localdb/bin/localdbtool-retrieve init
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017/localdb
#DB INFO# ---> Connection is GOOD.
#DB INFO# -----------------------
$
$./bin/dbAccessor -I
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# Local DB Server: mongodb://127.0.0.1:27017/localdb
#DB INFO# ---> connection is good.
#DB INFO# -----------------------
```

If an error occurs, please check [FAQ]().

### Local DB Tools

There are more three Local DB tools:

* Viewer Application
* Synchronization Tool
* Archive Tool

#### 1. Set-up Local DB Tools

##### Viewer Application

`localdb-tools/viewer/setup_viewer.sh` can set-up Viewer Application setting in user local environments by following steps:

* Create the viewer config file ---> [localdb-tools/viewer/conf.yml](config.md)
* Check if required python modules are installed

```bash
$ cd localdb-tools/viewer
$ ./setup_viewer.sh
<some texts>
[LDB] Are you sure that is correct? [y/n]
> y
<some texts>
[LDB] More information: https://localdb-docs.readthedocs.io/en/master/
```

**Additional options**

- **-i ``<IP address>``** : Set Local DB server IP address (default: 127.0.0.1)
- **-p ``<port>``** : Set Local DB server port (default: 27017)
- **-c ``<cfg>``** : Set config file Name (default: conf.yml)

##### Synchronization Tool

`localdb-tools/sync-tool/setup_sync_tool.sh` can set-up Synchronization Tool setting in user local environments by following steps:

* Create the sync config file ---> [localdb-tools/sync-tool/my_configure.yml](config.md)
* Edit config file automatically
* Check if required python modules are installed

```bash
$ cd localdb-tools/sync-tool
$ ./setup_sync_tool.sh
<some texts>
[LDB] Set editor command ... > vim
<some texts>
[LDB] More information: https://localdb-docs.readthedocs.io/en/master/
```

##### Archive Tool

`localdb-tools/sync-tool/setup_archive_tool.sh` can set-up Archiving Tool setting in user local environments by following steps:

* Create the archive config file ---> [localdb-tools/archive-tool/my_configure.yml](config.md)
* Edit config file automatically

```bash
$ cd localdb-tools/archive-tool
$ ./setup_archive_tool.sh
<some texts>
[LDB] Set editor command ... > vim
<some texts>
[LDB] More information: https://localdb-docs.readthedocs.io/en/master/
```

#### 2. Confirmation

##### Viewer Application

in edit.

##### Synchronization Tool

in edit.

##### Archive Tool

in edit.
