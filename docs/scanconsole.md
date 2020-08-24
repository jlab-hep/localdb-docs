# scanConsole

The **scanConsole** is the main read-out program in [YARR](https://yarr.readthedocs.io/en/latest/).

Contents:

1. [Getting Start](#1-getting-start)
2. [Usage](#2-usage)
3. [FAQ](#3-faq)

## 1. Getting Start

#### 0. Install & Setup

Please check [Pre Requirements](installation.md) to install required packages.<br>

First, please be sure to build YARR SW:

```bash
$ cd YARR
$ mkdir build && cd build
$ cmake3 ../
$ make -j4
```
> [More detail about YARR SW](https://yarr.readthedocs.io/en/latest/)

Next, please be sure to setup Local DB setting using `YARR/localdb/setup_db.sh`. <br>
This script confirms

- if the python packages is satisfied
- if the default config files are prepared
    - HOME/.yarr/localdb/HOSTNAME_database.json
    - HOME/.yarr/localdb/user.json
    - HOME/.yarr/localdb/HOSTNAME_site.json
- if the command is enabled
- if the DB connection is established

```bash
$ cd YARR
$ ./localdb/setup_db.sh

< Setting up with some texts >
```
> [More detail about setup_db.sh](setup-db.md)

#### 1. Confirmation

Please run the command with the emulator to check if the SW is available without uploading.<br>
This does not use or require any hardware and will run purely in software.<br>

```bash
$ cd YARR
$ bin/scanConsole \
-r configs/controller/emuCfg_rd53a.json \
-c configs/connectivity/example_rd53a_setup.json \
-s configs/scans/rd53a/std_digitalscan.json \
-p
```

Please run the command 'dbAccessor -I' to check if the command is working and the connection to Local DB is good.

```bash
$ ./bin/dbAccessor -I

#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017/localdb
#DB INFO# ---> Connection is GOOD.
#DB INFO# -----------------------
```

**Additional options**

- **-d ``<database.json>``**<br> : Set [database config file](config.md) (default: `HOME/.yarr/localdb/HOSTNAME_database.json`)

## 2. Usage

You can scan and upload test data by `scanConsole -W`:

```bash
$ ./bin/scanConsole \
-r configs/controller/emuCfg_rd53a.json \
-c configs/connectivity/example_rd53a_setup.json \
-s configs/scans/rd53a/std_digitalscan.json \
-W
<lots of text>
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017/localdb
#DB INFO# ---> Connection is GOOD.
#DB INFO# -----------------------
#DB INFO# Uploading in the back ground. (log: ~/.yarr/localdb/log/)
```

**Additional options**

- **-d ``<database cfg>``**<br> : Set [database config file](config.md) (default: `${HOME}/.yarr/localdb/${HOSTNAME}_database.json`)
- **-u ``<user cfg>``**<br> : Set [user config file](config.md)
- **-i ``<site cfg>``**<br> : Set [site config file](config.md)

## 3. FAQ

in edit.
