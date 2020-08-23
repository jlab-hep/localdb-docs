## dbAccessor -C

Contents:

1. [Synopsis](#1-synopsis)
2. [Installation](#2-installation)
3. [Syntax](#3-syntax)
4. [Examples](#4-examples)
5. [FAQ](#5-faq)

### 1. Synopsis

Basically component data is registered on ITk PD, and Local DB downloads and uses it.<br>
But if you want to manage non-QC component data, You can register component data by [dbAccessor -C](accessor-c.md)

### 2. Installation

The DB Accessor is included as part of [YARR SW](https://yarr.readthedocs.io/en/latest/).<br>
Follow the [dbAccessor Guide](accessor.md) to setup the command.

### 3. Syntax

The [dbAccessor -C](accessor-c.md) command has the following form:

```bash
$ ./bin/dbAccessor -C
                   [-c <path/to/component.json>]
```

**Command Line Arguments**

- **``-C``** <br>
Sets command to download scan data.
- **``-c <path>``**<br>
Specifies the path to [component config file](config.md) to register.<br>
The [component config](config.md) is similar as the [connectivity config](config.md) but need to fill "serialNumber" and "chipId" of the component.

**Additional options**

- **``-d <path>``**<br>
Specifies the path to [database config file](database-config.md).<br>
If -d is not specified, dbAccessor sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](database-config.md).
- **``-u <path>``**<br>
Specifies the path to [user config file](user-config.md)<br>
If -u is not specified, dbAccessor sets `HOME/.yarr/localdb/user.json` as [user config file](user-config.md).
- **``-i <path>``**<br>
Specifies the path to [site config file](site-config.md)<br>
If -i is not specified, dbAccessor sets `HOME/.yarr/localdb/HOSTNAME_site.json` as [site config file](site-config.md).

### 4. Examples


### 5. FAQ
