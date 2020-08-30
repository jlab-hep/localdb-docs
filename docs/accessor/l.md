# dbAccessor -L

### Table of Contents

1. [Synopsis](#1-synopsis)
2. [Installation](#2-installation)
3. [Syntax](#3-syntax)
4. [Examples](#4-examples)
5. [FAQ](#5-faq)

## 1. Synopsis

You can check the test log registered in Local DB.

## 2. Installation

The DB Accessor is included as part of [YARR SW](http://yarr.web.cern.ch/yarr/).<br>
Follow the [dbAccessor Guide](../accessor.md) to setup the command.

## 3. Syntax

The [dbAccessor -L](l.md) command has the following form:

```bash
$ ./bin/dbAccessor -L
                   [-n <component name>]
                   [-u <user name>]
                   [-i <site name>]
                   [-d <path/to/database.json>]
```

**Command Line Arguments**

- **``-L``**<br>
Sets command to display test data

**Additional options**

- **``-n <name>``**<br>
Specifies the component name to query.

- **``-u <name>``**<br>
Specifies the user name to query.

- **``-i <name>``**<br>
Specifies the site name to query.

- **``-d <path>``**<br>
Specifies the path to [database config file](../config/database.md).<br>
If -d is not specified, dbAccessor sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](../config/database.md).

## 4. Examples

```bash
$ ./bin/dbAccessor -L
[  info  ]: DBHandler: Retrieve Test Log
[  info  ]: -----------------------
[  info  ]: Checking connection to DB Server: mongodb://127.0.0.1:30000/localdb ...
[  info  ]: Checking connection to DB Server: mongodb://127.0.0.1:27017/localdb ...
[  info  ]: ---> Good connection!
test data ID: 5f46102aeb314f894100823e
User      : username at site
Date      : 2020/08/26 16:32:35
Component : JohnDoe_0
Run Number: 6220
Test Type : std_digitalscan
DCS Data  :
   vddd_voltage (JohnDoe_0)

test data ID: 5f45f9a7af458eb989840b5e
User      : username at site
Date      : 2020/08/26 14:56:31
Component : 20UPGRS0000039, 20UPGRA0001996
Run Number: 6213
Test Type : std_digitalscan
DCS Data  : NULL
```
