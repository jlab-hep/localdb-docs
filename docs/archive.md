# Archive Tool

The **Archive Tool** creates a/some archive tar.gz files to back-up Local DB.

### Table of Contents

1. [Command](#1-command)
2. [Getting Start](#2-getting-start)
3. [Usage](#3-usage)
4. [FAQ](#4-faq)

## 1. Command

- Location: **localdb-tools/archive-tool/bin/localdbtool-archive.sh**
- Syntax:

```bash
$ cd localdb-tools/archivee-tool
$ ./bin/localdbtool-archive.sh
```

## 2. Getting start

The archive tool is included as part of [Local DB Tools](https://gitlab.cern.ch/YARR/localdb-tools).<br>
Follow the [installtaion tutorial](installation.md) to install required packages.

#### 1. Setup

Setup the configuration files of the archive tool using [localdb-tools/archive-tool/setup_archive_tool.sh](script/setup_archive_tool.md) shell:

```bash
$ cd localdb-tools/archivee-tool
$ ./setup_archive_tool.sh
```

## 3. Usage

#### a. Keep backup to .tar.gz file

```bash
$ cd localdb-tools/archive-tool
$ ./bin/localdbtool-archive.sh -f my_archive_configure.yml
```

###### Command Line Arguments

* **``-f|--config <config file>``**<br>
Specifies path to [configure file](config/archive.md)

- **``-p|--db-port <port>``**<br>
Specifies Local DB server port (default: **27017)

- **``-d|--db-name <name>``**<br>
Specifies Local DB name (default: localdb)

* **``-a|--archive-path <dir>``**<br>
Specifies directory path to archives will be put (default: ./archive-mongo-data)

* **``-l|--log <dir>``**<br>
Specifies directory path to log files will be put (default: ./log)

* **``-n|--n-archives <num>``**<br>
Specifies # of archives to keep (default: 2)

#### b. Restore DB from .tar.gz file

**Local DB will be override**<br>
**Please be sure to keep backup before restoring**

```bash
$ cd localdb-tools/archive-tool
$ tar -zxvf archive-mongo-data/dump_191128_143352.tar.gz
$ mongorestore --db localdb dump_191128_143352/localdb
$ mongorestore --db localdbtools dump_191128_143352/localdbtools
$ rm -rf dump_191128_143352
```

## 4. FAQ

in edit.
