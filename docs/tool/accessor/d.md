# dbAccessor -D

### Table of Contents

1. [Synopsis](#1-synopsis)
2. [Installation](#2-installation)
3. [Syntax](#3-syntax)
4. [Examples](#4-examples)
5. [FAQ](#5-faq)

## 1. Synopsis

You can retrieve scan data from Local DB by [dbAccessor -D](d.md)

## 2. Installation

The DB Accessor is included as part of [YARR SW](http://yarr.web.cern.ch/yarr/).<br>
Follow the [dbAccessor Guide](../accessor.md) to setup the command.

## 3. Syntax

The [dbAccessor -D](d.md) command has the following form:

```bash
$ ./bin/dbAccessor -D
                   [-n <component name>]
                   [-p <path/to/output/dir>]
                   [-c <path/to/component.json>]
                   [-d <path/to/database.json>]
```

**Command Line Arguments**

- **``-D``** <br>
Sets command to download scan data.

**Additional options**

- **``-n <name>``**<br>
Specifies the component name to link the DCS data.
- **``-p <path>``**<br>
Specifies the path to directory to output retrieved data.<br>
If -p is not specified, dbAccessor sets `./db-data` as directory to output.
- **``-c <path>``**<br>
Specifies the path to [component connectivity config file](../../config/connectivity.md).<br>
You can create chip config files with filling chip names and chip IDs <br>
according the specified connectivity config even if the chips are not registered in Local DB.
- **``-d <path>``**<br>
Specifies the path to [database config file](../../config/database.md).<br>
If -d is not specified, dbAccessor sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](../../config/database.md).

## 4. Examples

in edit.
