# Archive Tool

The **archive-tool** creates a/some archive tar.gz files to back-up Local DB.

Contents:

0. [Command](#0-command)
1. [Getting Start](#1-getting-start)
2. [Usage](#2-usage)
3. [FAQ](#3-faq)

## 0. Command

**localdb-tools/archive-tool/bin/localdbtool-archive.sh**

```bash
$ ./bin/localdbtool-archive.sh

# optional arguments:
# -h --help         : show help
# -f --config       : config path
# -p --db-port      : database port         (default. 27017)
# -d --db-name      : database name         (default. localdb)
# -a --archive_path : archive path          (default. ./archive-mongo-data)
# -l --log          : log path              (default. ./log)
# -n --n_archives   : # of archives to keep (default. 2)
```

## 1. Getting start

Please check [Pre Requirements](requirements.md) to install required packages.<br>
And please be sure to setup Archive Tool setting using `localdb-tools/archive-tool/setup_archive_tool.sh`. <br>
This script performs

- to confirm the config file ( [localdb-tools/archive-tool/my_archive_configure.yml](config.md) )
- to set the binary command in bin directory

```bash
$ cd localdb-tools/archive-tool
$ ./setup_archive_tool.sh
< Setting up with some texts >
```

## 2. Usage

### a. Keep backup to .tar.gz file

```bash
$ cd localdb-tools/archive-tool
$ ./bin/localdbtool-archive.sh -f my_archive_configure.yml
```

**Command Line Arguments**

* **-f|--config ``<config file>``**<br> : Set path to [configure file](config.md)
- **-p|--db-port ``<port>``**<br> : Set Local DB server port (default: 27017)
- **-d|--db-name ``<name>``**<br> : Set Local DB name (default: localdb)
* **-a|--archive-path ``<dir>``**<br> : Set directory path to archives will be put (default: ./archive-mongo-data)
* **-l|--log ``<dir>``**<br> : Set directory path to log files will be put (default: ./log)
* **-n|--n-archives ``<num>``**<br> : Set # of archives to keep (default: 2)

### b. Restore DB from .tar.gz file

**Local DB will be override**<br>
**Please be sure to keep backup before restoring**

```bash
$ cd localdb-tools/archive-tool
$ tar -zxvf archive-mongo-data/dump_191128_143352.tar.gz
$ mongorestore --db localdb dump_191128_143352/localdb
$ mongorestore --db localdbtools dump_191128_143352/localdbtools
$ rm -rf dump_191128_143352
```

## 3. FAQ

in edit.
