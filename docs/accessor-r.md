# dbAccessor -R

### Table of Contents

1. [Synopsis](#1-synopsis)
2. [Installation](#2-installation)
3. [Syntax](#3-syntax)
4. [Examples](#4-examples)
5. [FAQ](#5-faq)

## 1. Synopsis

When you could not upload scan/DCS data because of the bad connection to Local DB server,
the cache data and log file ([scanLog.json](scan-log.md)/[dbDcsLog.json](config.md)) would be stored in the result directory,
and the record is written to the file: `HOME/.yarr/run.dat`/`HOME/.yarr/dcs.dat`.

You can upload all cache data into Local DB when the good connection to Local DB server by [dbAccessor-R](accessor-r.md)

## 2. Installation

The DB Accessor is included as part of [YARR SW](https://yarr.readthedocs.io/en/latest/).<br>
Follow the [dbAccessor Guide](accessor.md) to setup the command.

## 3. Syntax

The [dbAccessor -R](accessor-r.md) command has the following form:

```bash
$ ./bin/dbAccessor -R
                   [-d <path/to/database.json>]
                   [-u <path/to/user.json>]
                   [-i <path/to/site.json>]
                   [-Q]
                   [-I]
```

**Command Line Arguments**

- **``-R``**<br>
Sets command to upload cache data

**Additional options**

- **``-d <path>``**<br>
Specifies the path to [database config file](database-config.md).<br>
If -d is not specified, dbAccessor sets the path of "dbCfg" written in [scanLog.json](scan-log.md) located in the specified scan result directory,<br>
or sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](database-config.md) if no "dbCfg" written in [scanLog.json](scan-log.md).
- **``-u <path>``**<br>
Specifies the path to [user config file](user-config.md)<br>
If -u is not specified, dbAccessor sets the path of "userCfg" written in [scanLog.json](scan-log.md) located in the specified scan result directory,<br>
or sets `HOME/.yarr/localdb/user.json` as [user config file](user-config.md) if no "userCfg" written in [scanLog.json](scan-log.md).
- **``-i <path>``**<br>
Specifies the path to [site config file](site-config.md)<br>
If -i is not specified, dbAccessor sets the path of "siteCfg" written in [scanLog.json](scan-log.md) located in the specified scan result directory,<br>
or sets `HOME/.yarr/localdb/HOSTNAME_site.json` as [site config file](site-config.md) if no "siteCfg" written in [scanLog.json](scan-log.md).
- **``-Q``**<br>
Sets QC mode and add a step to check if the data to upload is suitable for QC.
- **``-I``**<br>
Sets interactive mode and add a step to ask the user to check the data to upload interactively.

## 4. Examples

in edit.
