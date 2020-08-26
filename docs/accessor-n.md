# dbAccessor -N

### Table of Contents

1. [Synopsis](#1-synopsis)
2. [Installation](#2-installation)
3. [Syntax](#3-syntax)
4. [Examples](#4-examples)

## 1. Synopsis

You can check if the command is working and if the connection to Local DB is good.

## 2. Installation

The DB Accessor is included as part of [YARR SW](https://yarr.readthedocs.io/en/latest/).<br>
Follow the [dbAccessor Guide](accessor.md) to setup the command.

## 3. Syntax

The [dbAccessor -N](accessor-n.md) command has the following form:

```bash
$ ./bin/dbAccessor -N
                   [-d <path/to/database.json>]
```

###### Command Line Arguments

- **``-N``**<br>
Sets command to check the connection to Local DB.

###### Additional options

- **``-d <path>``**<br>
Specifies the path to [database config file](database-config.md).<br>
If -d is not specified, dbAccessor sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](database-config.md).

## 4. Examples

#### Normal Usage

```bash
$ ./bin/dbAccessor -N
[  info  ]: DBHandler: Check DB Connection
[  info  ]: ------------------------------
[  info  ]: Function: Initialize upload function and check connection to Local DB
[  info  ]: -> Setting database config: /home/example/.yarr/localdb/localhost_database.json
[  info  ]: Checking connection to DB Server: mongodb://127.0.0.1:27017/localdb ...
[  info  ]: ---> Good connection!
[  info  ]: ------------------------------
```

The output of "Good connection!" means that the connection to Local DB is successful
and the database access functions such as uploading and downloading data are available.

#### Use with specifying a database config file

```bash
$ ./bin/dbAccessor -N -d database.json
[  info  ]: DBHandler: Check DB Connection
[  info  ]: ------------------------------
[  info  ]: Function: Initialize upload function and check connection to Local DB
[  info  ]: -> Setting database config: /home/example/YARR/database.json
[  info  ]: Checking connection to DB Server: mongodb://127.0.0.1:27017/localdb ...
[  info  ]: ---> Good connection!
[  info  ]: ------------------------------
```

Make sure the [database config file](database-config.md) exists in the specified path.<br>
If the file does not exist or unreadable as a JSON file, dbAccessor returns error.<br>
If you get an error, follow [FAQ for dbAccessor](accessor-faq.md#not-found-xxx) to resolve it.
