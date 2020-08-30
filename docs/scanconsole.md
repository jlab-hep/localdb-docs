# scanConsole

The **scanConsole** is the main read-out program in [YARR](http://yarr.web.cern.ch/yarr/).

### Table of Contents

1. [Command](#1-command)
2. [Getting Start](#2-getting-start)
3. [Syntax](#3-syntax)
4. [Examples](#4-examples)
5. [FAQ](#5-faq)

## 1. Command

- Location: **YARR/bin/scanConsole**
- Syntax:

```bash
$ cd YARR
$ ./bin/scanConsole [-option]
```

## 2. Getting Start

#### 0. Install & Setup

The DB Accessor is included as part of [YARR SW](https://gitlab.cern.ch/YARR/YARR).<br>
Follow the [installation tutorial](installation.md) to install required packages and make sure to build YARR SW:

```bash
$ cd YARR
$ mkdir build && cd build
$ cmake3 ../
$ make -j4
cd ../
```

And make sure to setup Local DB configuration files using [YARR/localdb/setup_db.sh](script/setup-db.md) shell:

```bash
$ ./localdb/setup_db.sh
```

#### 1. Confirmation

You can run the [scanConsole](scanconsole.md) with the emulator to check if the command is working.<br>
This does not use/require any hardware and will run purely in software:

```bash
$ bin/scanConsole \
-r configs/controller/emuCfg_rd53a.json \
-c configs/connectivity/example_rd53a_setup.json \
-s configs/scans/rd53a/std_digitalscan.json \
-p
```

And run the [DB Accessor](accessor.md) with command-line option **-N** to check if the command is working and the connection to Local DB is good:

```bash
$ ./bin/dbAccessor -N
```

## 3. Syntax

The [scanConsole](scanconsole.md) command to use the Local DB related functions has the following form:

```bash
$ ./bin/scanConsole -r <path/to/controller.json>
                    -c <path/to/connectivity.json>
                    -s <path/to/scan.json>
                    -W
                    [-Q]
                    [-I]
                    [-d <path/to/database.json>]
                    [-u <path/to/user.json>]
                    [-i <path/to/site.json>]
```

###### Command Line Arguments

- **``-r <path>``**<br>
Specifies the path to controller config. (e.g. YARR/configs/controller/specCfg.json)

- **``-c <path>``**<br>
Specifies the path to [connectivity config](config/connectivity.md). (e.g. YARR/configs/connectivity/example_xxx_setup.json)

- **``-s <path>``**<br>
Specifies the path to scan config. (e.g. YARR/configs/scans/xxx/std_digitalscan.json)

- **``-W``**<br>
Sets command to upload results into Local DB after the scan.

###### Additional options

- **``-Q``**<br>
Enables QC mode which adds a strict verification step before running scan.<br>
If the files are unsuitable for QC, exit the scan.<br>
_This option cannot be enabled without -W option._

- **``-I``**<br>
Enables interactive mode which adds a confirmation step by the user before running scan.<br>
_This option cannot be enabled without -W option._

- **``-d <path>``**<br>
Specifies the path to [database config file](config/database.md).<br>
If -d is not specified, scanConsole sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](config/database.md).

- **``-u <path>``**<br>
Specifies the path to [user config file](config/user.md)<br>
If -u is not specified, scanConsole sets `HOME/.yarr/localdb/user.json` as [user config file](config/user.md).

- **``-i <path>``**<br>
Specifies the path to [site config file](config/site.md)<br>
If -i is not specified, scanConsole sets `HOME/.yarr/localdb/HOSTNAME_site.json` as [site config file](config/site.md).

## 4. Examples

```bash
$ ./bin/scanConsole \
-r configs/controller/emuCfg_rd53a.json \
-c configs/connectivity/example_rd53a_setup.json \
-s configs/scans/rd53a/std_digitalscan.json \
-W
<lots of text>
[  info  ]: Succeeded uploading scan data from /home/work/YARR/data/000004_std_digitalscan
```
The output of "Succeeded uploading" means that data was uploaded into Local DB successfully.

## 5. FAQ

in edit.
