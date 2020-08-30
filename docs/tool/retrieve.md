# Retrieve Tool

The **Retrieve Tool** is to retrieve data from Local DB.

### Table of Contents

1. [Command](#1-command)
2. [Getting Start](#2-getting-start)
3. [Usage](#3-usage)
4. [FAQ](#4-faq)

---

# 1. Command

- Location: **YARR/localdb/bin/localdb-retrieve**
- Syntax:

```bash
./localdb/bin/localdbtool-retrieve <option>
                                   [--config <CONFIG>]
                                   [--username <USERNAME>]
                                   [--password <PASSWORD>]
                                   [--database <DATABASE>]
                                   [--user <USER>]
                                   [--site <SITE>]
                                   [--chip <CHIP>]
                                   [--test <TEST>]
                                   [--directory <DIRECTORY>]
                                   [--config_only]
                                   [--create_config <CONN>]
                                   [--QC]
#positional arguments:
#  command               option*	funtion
#                        init	Function initialization & Connection check
#                        log	Display data log
#                        pull	Data retrieve
#                        list	Display data list
#                        user	Get user&site data
#
#optional arguments:
#  -h, --help            show this help message and exit
#  --config CONFIG       Set User Config Path of Local DB Server.
#  --username USERNAME   Set the User Name of Local DB Server.
#  --password PASSWORD   Set the Password of Local DB Server.
#  --database DATABASE   Set Database Config Path
#  --user USER           Set the name of the user.
#  --site SITE           Set the name of the site.
#  --chip CHIP           Set the name of the chip.
#  --test TEST           Set data ID of the test.
#  --directory DIRECTORY
#                        Provide directory name.
#  --config_only         Set mode to pull config files only.
#  --create_config CREATE_CONFIG
#                        Set path to connectivity config to create chip config files.
#  --QC                  Set QC Mode
```

## 2. Getting start

#### 0. Install & Setup

The DB Accessor is included as part of [YARR SW](https://gitlab.cern.ch/YARR/YARR).<br>
Follow the [installation tutorial](../installation.md) to install required packages and make sure to setup Local DB configuration files using [YARR/localdb/setup_db.sh](../script/setup-db.md) shell:

```bash
$ cd YARR
$ ./localdb/setup_db.sh
```

#### 1. Confirmation

Run the command with the option 'init' to check if the command is working and the connection to Local DB is good.

```bash
$ ./localdb/bin/localdbtool-retrieve init
[  info  ]: Checking connection to DB Server: mongodb://127.0.0.1:27017/localdb ...
[  info  ]: ---> Good connection!
[  info  ]: ------------------------------
```

## 3. Usage

Retrieve Tool performs following functions:

* [Retrieve the uploaded test data log](#retrieve-test-log)
* [Retrieve the uploaded data into local directory](#retrieve-data-files)
* [Retrieve the uploaded data list](#retrieve-data-list)
* [Create the config files for the registered component data](#create-config)
* [Check the user config and site config for QC](#check-user-site-config)

### Retrieve test log

You can check uploaded test log in command line by `localdbtool-retrieve log`:

```bash
$ ./localdb/bin/localdbtool-retrieve log
test data ID: 5d4c94c1fd212a639247b044
User      : arisa_kubota at tokyo_institute_of_technology
Date      : 2019/08/08 14:31:39
Chip      : RD53A-001, RD53A-001_chip1
Run Number: 255
Test Type : std_analogscan
DCS Data  : NULL
# Ctrl+C can terminate the output
```

###### Command Line Arguments

- **``--database <database cfg>``**<br>
Set [database config file](../config/database.md) (default: `HOME/.yarr/localdb/HOSTNAME_database.json`)
- **``--username <username>``**<br>
Set username of the Local DB Server if the user authentication is required
- **``--password <password>``**<br>
Set password of the Local DB Server if the user authentication is required
- **``--config <config file>``**<br>
Set config file which username and password are written in if the user authentication is required
- **``--user <user name>``**<br>
Set the user name to query
- **``--site <site name>``**<br>
Set the site name to query
- **``--chip <chip name>``**<br>
Set the chip name to query

### Retrieve data files

You can retrieve the uploaded data into the local directory by `localdbtool-retrieve pull`:

```bash
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
#DB INFO# Retrieve ... ./db-data/ctrlCfg.json
#DB INFO# Retrieve ... ./db-data/dbCfg.json
#DB INFO# Retrieve ... ./db-data/siteCfg.json
#DB INFO# Retrieve ... ./db-data/userCfg.json
#DB INFO# Retrieve ... ./db-data/std_digitalscan.json
#DB INFO# Retrieve ... ./db-data/scanLog.json
#DB INFO# Retrieve ... ./db-data/JohnDoe_0_EnMask.dat
#DB INFO# Retrieve ... ./db-data/JohnDoe_0_OccupancyMap.dat
#DB INFO# Retrieve ... ./db-data/JohnDoe_0_beforeCfg.json
#DB INFO# Retrieve ... ./db-data/fei4b_test.json
#DB INFO# Retrieve ... ./db-data/JohnDoe_0_afterCfg.json
#DB INFO# Retrieve ... ./db-data/connectivity.json
#DB INFO# -----------------------
```

###### Command Line Arguments

- **``--database <database cfg>``**<br>
Set [database config file](../config/database.md) (default: `HOME/.yarr/localdb/HOSTNAME_database.json`)
- **``--username <username>``**<br>
Set username of the Local DB Server if the user authentication is required
- **``--password <password>``**<br>
Set password of the Local DB Server if the user authentication is required
- **``--config <config file>``**<br>
Set config file which username and password are written in if the user authentication is required
- **``--chip <chip name>``**<br>
Set the chip name for specifying test data
- **``--test <test ID>``**<br>
Set the test ID for specifying test data
- **``--directory <path>``**<br>
Set the path to directory saving retrieved data

You can specify test data by setting the chip name with `--chip` or the test ID with `--test`. <br>
If you set the chip name, you can retrieve the latest test data for the chip.<br>
If you set the test ID (which is document ID in Local DB you can check by `localdbtool-retrieve log`), you can retrieve the test data with the ID.<br>

* List of restored data (default output dir: `YARR/db_data`)
    * Test Information (Data ID, User, Date, Chips, Run #, Test type)
    * connectivity config file
    * controller config file
    * scan config file
    * chip config file (original/before/after)
    * result data file
    * database config file
    * user config file
    * site config file

### Retrieve data list

You can retrieve the uploaded data (component, user, site) by `localdbtool-retrieve list <opt>`.

#### 1. Component list (default)

```bash
$ ./localdb/bin/localdbtool-retrieve list

hybrid: 1012
User      : arisa_kubota at lawrence_berkeley_national_laboratory
Chip Type : RD53A
Chips(3)  :
    front-end_chip: 0x0438
    User  : arisa_kubota at lawrence_berkeley_national_laboratory
    ChipId: 1
    front-end_chip: 0x044B
    User  : arisa_kubota at lawrence_berkeley_national_laboratory
    ChipId: 2
    front-end_chip: 0x0446
    User  : arisa_kubota at lawrence_berkeley_national_laboratory
    ChipId: 4
# Ctrl+C can terminate the output
```

#### 2. User list

```bash
$ ./localdb/bin/localdbtool-retrieve list user

User Name: kubota
- lazulite

User Name: akubota
- Tokyo Institute of Technology

User Name: arisa_kubota
- tokyo_institute_of_technology
# Ctrl+C can terminate the output
```

#### 3. Site list

```bash
$ ./localdb/bin/localdbtool-retrieve list site

- Tokyo Institute of Technology
- lawrence_berkeley_national_laboratory
# Ctrl+C can terminate the output
```

### Create Config

You can create the connectivity config file and the chip config files after the component registration. <br>
The component data can be registered by [DB Accessor](accessor.md) or can be downloaded from ITkPD by [ITkPD Interface](itkpd-interface.md). <br>
You can create the config files by `localdb-retrieve pull --chip <SERIAL NUMBER>`.<br>
If you have already uploaded the component test data, the config files in the latest scan are retrieved.

```bash
$ ./localdb/bin/localdb-retrieve pull --chip <SERIAL NUMBER> --config_only
#DB INFO# -----------------------
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017/localdb
#DB INFO# ---> Connection is GOOD.
#DB WARNING# Not found test data of the component: <SERIAL NUMBER>
#DB INFO# component data ID: 5dce77c414dc504d3ad53e80
#DB INFO# - Name: <SERIAL NUMBER>  Type: RD53A
#DB INFO# Retrieve ... ./db-data/<SERIAL NUMBER>.json
#DB INFO# Retrieve ... ./db-data/connectivity.json
#DB INFO# -----------------------
```

* List of created config (default output dir: `YARR/db_data`)
    * connectivity config file
    * chip config file (copied from `YARR/configs/defaults/default_FE.json` with replacing `Name` and `ChipId`)

### Check User & Site Config

You can check your user config and site config for QC:

```bash
$ ./localdb/bin/localdbtool-retrieve user --QC
```

## 4. FAQ

in edit.
