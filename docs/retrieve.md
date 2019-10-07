# Retrieve Tool

This page describes how to retrieve data into Local DB.<br>
Please look at [Installation](install.md) to set-up Retrieve Tool.

## Check Command & Connection

```bash
$ cd <YARR SW installation dir>
$ ./localdb/bin/localdbtool-retrieve init
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# Local DB Server: mongodb://127.0.0.1:27017/localdb
#DB INFO# ---> connection is good.
#DB INFO# -----------------------
```

#### Additional options

- **--database ``<database cfg>``** : Set database config file (default: `${HOME}/.yarr/localdb/${HOSTNAME}_database.json`)

## Retrieve test log

You can check uploaded test log in command line by `localdbtool-retrieve log`:

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
# Ctrl+C can terminate the output
```

#### Additional options

- **--database ``<database cfg>``** : Set database config file (default: `${HOME}/.yarr/localdb/${HOSTNAME}_database.json`)
- **--username ``<username>``** : Set username of the Local DB Server if the user authentication is required 
- **--password ``<password>``** : Set password of the Local DB Server if the user authentication is required 
- **--config ``<config file>``** : Set config file which username and password are written in if the user authentication is required
- **--user ``<user name>``** : Set the user name for refine search
- **--site ``<site name>``** : Set the site name for refine search
- **--chip ``<chip name>``** : Set the chip name for refine search

## Retrieve data files

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

#### Additional options

- **--database ``<database cfg>``** : Set database config file (default: `${HOME}/.yarr/localdb/${HOSTNAME}_database.json`)
- **--username ``<username>``** : Set username of the Local DB Server if the user authentication is required 
- **--password ``<password>``** : Set password of the Local DB Server if the user authentication is required 
- **--config ``<config file>``** : Set config file which username and password are written in if the user authentication is required
- **--chip ``<chip name>``** : Set the chip name for specifying test data
- **--test ``<test ID>``** : Set the test ID for specifying test data
- **--directory ``<path>``** : Set the path to directory saving retrieved data

You can specify test data by setting the chip name with `--chip` or the test ID with `--test`.
If you set the chip name, you can retrieve the latest test data for the chip.
If you set the test ID (which is document ID in Local DB you can check by `localdbtool-retrieve log`), you can retrieve the test data with the ID.

* List of restored data (default dir: `YARR/db_data`)
    * Test Information (Data ID, User, Date, Chips, Run #, Test type) 
    * connectivity config file
    * controller config file
    * scan config file
    * chip config file (original/before/after)
    * result data file
    * database config file
    * user config file
    * site config file

## Retrieve data list

You can retrieve the uploaded data (component, user, site) by `localdbtool-retrieve list <opt>`: 
 
### Component list (default)

```bash
$ ./localdb/bin/localdbtool-retrieve list 
#DB INFO# -----------------------
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017
#DB INFO#    The connection is GOOD.

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

hybrid: 1011 
User      : arisa_kubota at lawrence_berkeley_national_laboratory
Chip Type : RD53A
Chips(3)  :
    front-end_chip: 0x0439 
    User  : arisa_kubota at lawrence_berkeley_national_laboratory
    ChipId: 1
    front-end_chip: 0x044A 
    User  : arisa_kubota at lawrence_berkeley_national_laboratory
    ChipId: 2
    front-end_chip: 0x0445 
    User  : arisa_kubota at lawrence_berkeley_national_laboratory
    ChipId: 4
# Ctrl+C can terminate the output
```


### User list

```bash
$ ./localdb/bin/localdbtool-retrieve list user
#DB INFO# -----------------------
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017
#DB INFO#    The connection is GOOD.

User Name: kubota
- lazulite

User Name: akubota
- Tokyo Institute of Technology

User Name: arisa_kubota
- tokyo_institute_of_technology
# Ctrl+C can terminate the output 
```

### Site list

```bash
$ ./localdb/bin/localdbtool-retrieve list site
#DB INFO# -----------------------
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017
#DB INFO#    The connection is GOOD.

- Tokyo Institute of Technology
- lawrence_berkeley_national_laboratory
# Ctrl+C can terminate the output
```
