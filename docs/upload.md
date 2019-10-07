# Upload Tool

This page describes how to upload data into Local DB.<br>
Please look at [Installation](install.md) to set-up Upload Tool.

## Check Command & Connection

```bash
$ cd <YARR SW installation dir>
$ ./localdb/bin/localdbtool-upload init
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# Local DB Server: mongodb://127.0.0.1:27017/localdb
#DB INFO# ---> connection is good.
#DB INFO# -----------------------
```

Additional options:

- **--database ``<database cfg>``** : Set database config file (default: `${HOME}/.yarr/localdb/${HOSTNAME}_database.json`)

## Upload test data

There are two ways to upload test data into Local DB:

* `scanConsole -W` to upload test data after scanConsole immediately
* `localdbtool-upload scan` to upload test data from the specific result directory

### scanConsole -W

You can scan and upload test data by `scanConsole -W`

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

Additional options:

- **-d ``<database cfg>``** : Set database config file (default: `${HOME}/.yarr/localdb/${HOSTNAME}_database.json`)
- **-u ``<user cfg>``** : Set user config file
- **-i ``<site cfg>``** : Set site config file

### localdbtool-upload scan

You can upload test data from the specific result directory by `localdbtool-upload scan`.

```bash
$ ./localdb/bin/localdbtool-upload scan <path/to/result/dir>
e.g.) $ ./localdb/bin/localdbtool-upload scan ./data/last_scan
```

Additional options:

- **--database ``<database cfg>``** : Set database config file (default: `${HOME}/.yarr/localdb/${HOSTNAME}_database.json`)
- **--user ``<user cfg>``** : Set user config file
- **--site ``<site cfg>``** : Set site config file
- **--log** : Set logging mode (default 'False'). If set 'True', the output log is written in `${HOME}/.yarr/localdb/log/${day}.log`
- **--username ``<username>``** : Set username of the Local DB Server if the user authentication is required 
- **--password ``<password>``** : Set password of the Local DB Server if the user authentication is required 
- **--config ``<config file>``** : Set config file which username and password are written in if the user authentication is required

## Upload cache data

When you could not upload Scan/DCS data by `scanConsole -W`/`dbAccessor -E` because of the bad connection to Local DB Server,
the cache data and log file ('scanLog.json'/'dbDcsLog.json') would be stored i the result directory,
and that record is written to the file: `${HOME}/.yarr/run.dat`/`${HOME}/.yarr/dcs.dat`.

If the good connection to Local DB Server, you can upload all cache data by `localdbtool-upload cache`:

```bash
$ ./localdb/bin/localdbtool-upload cache
```

