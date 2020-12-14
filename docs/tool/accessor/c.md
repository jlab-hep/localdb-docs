# dbAccessor -C

### Table of Contents

1. [Synopsis](#1-synopsis)
2. [Installation](#2-installation)
3. [Syntax](#3-syntax)
4. [Examples](#4-examples)

## 1. Synopsis

Basically component data is registered on ITk PD, and Local DB downloads and uses it.<br>
But if you want to manage non-QC component data, You can register component data by [dbAccessor -C](c.md)

## 2. Installation

The DB Accessor is included as part of [YARR SW](http://yarr.web.cern.ch/yarr/).<br>
Follow the [dbAccessor Guide](../accessor.md) to setup the command.

## 3. Syntax

The [dbAccessor -C](c.md) command has the following form:

```bash
$ ./bin/dbAccessor -C
                   [-c <path/to/component.json>]
```

**Command Line Arguments**

- **``-C``** <br>
Sets command to download scan data.
- **``-c <path>``**<br>
Specifies the path to [component config file](../../config/component.md) to register.<br>
The [component config](../../config/component.md) is similar as the [connectivity config](../../config/connectivity.md) but need to fill "serialNumber" and "chipId" of the component.
- **``-u <path>``**<br>
Specifies the path to [user config file](../../config/user.md).
- **``-i <path>``**<br>
Specifies the path to [site config file](../../config/site.md).

**Additional options**

- **``-d <path>``**<br>
Specifies the path to [database config file](../../config/database.md).<br>
If -d is not specified, dbAccessor sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](../../config/database.md).

## 4. Examples

in edit.
