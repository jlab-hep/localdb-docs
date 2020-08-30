# dbAccessor -S

### Table of Contents

1. [Synopsis](#1-synopsis)
2. [Installation](#2-installation)
3. [Syntax](#3-syntax)
4. [Examples](#4-examples)

## 1. Synopsis

You can upload scan data from the specified scan result directory into Local DB.

## 2. Installation

The DB Accessor is included as part of [YARR SW](http://yarr.web.cern.ch/yarr/).<br>
Follow the [dbAccessor Guide](../accessor.md) to setup the command.

## 3. Syntax

The [dbAccessor -S](s.md) command has the following form:

```bash
$ ./bin/dbAccessor -S <path/to/result/dir>
                   [-d <path/to/database.json>]
                   [-Q]
                   [-I]
```

###### Command Line Arguments

- **``-S <path>``**<br>
Sets command to upload scan data and specifies the path to scan result directory to upload.<br>
Make sure the [scanLog.json](../config/scan-log.md) exists in the specified directory.

###### Additional options

- **``-d <path>``**<br>
Specifies the path to [database config file](../config/database.md).<br>
If -d is not specified, dbAccessor sets the path of "dbCfg" written in [scanLog.json](../config/scan-log.md) located in the specified scan result directory,
or sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](../config/database.md) if no "dbCfg" written in [scanLog.json](../config/scan-log.md).
- **``-Q``**<br>
Sets QC mode and add a step to check if the data to upload is suitable for QC.
- **``-I``**<br>
Sets interactive mode and add a step to ask the user to check the data to upload interactively.

## 4. Examples

#### Normal Usage

```bash
$ cd YARR
$ ./bin/scanConsole -c configs/connectivity/example_rd53a_setup.json -r configs/controller/specCfg.json -s configs/scans/rd53a/std_digitalscan.json -p
<lot texts>
./data/last_scan/JohnDoe_0_EnMask.png
./data/last_scan/JohnDoe_0_L1Dist.png
./data/last_scan/JohnDoe_0_OccupancyMap.png
```

When you scan, the result files are output in the directory `./data/<runnumber>`, which is symbolically linked to the directory `./data/last_scan`.<br>
You can upload the data from the result directory into Local DB by:

```bash
$ ./bin/dbAccessor -S data/last_scan/
[  info  ]: DBHandler: Register Scan Data
[  info  ]: ------------------------------
[  info  ]: Function: Upload scan data from specified directory
[  info  ]: Cache Directory: /home/example/YARR/data/006190_std_digitalscan
[  info  ]: -> Setting user config: /home/example/.yarr/localdb/user.json
[  info  ]: -> Setting site config: /home/example/.yarr/localdb/localhost_site.json
[  info  ]: -> Setting database config: /home/example/.yarr/localdb/localhost_database.json (default)
[  info  ]: Checking connection to DB Server: mongodb://127.0.0.1:27017/localdb ...
[  info  ]: ---> Good connection!
[  info  ]: Loading user information ...
[  info  ]: ~~~ {
[  info  ]: ~~~     ...
[  info  ]: ~~~ }
[  info  ]: Loading site information ...
[  info  ]: ~~~ {
[  info  ]: ~~~     ...
[  info  ]: ~~~ }
[  info  ]: Loading component information ...
[  info  ]: ~~~ {
[  info  ]: ~~~     ...
[  info  ]: ~~~ }
[  info  ]: Succeeded uploading scan data from /home/example/YARR/data/006190_std_digitalscan
[  info  ]: ------------------------------
```

The dbAccessor loads files in the specified directory while displaying the contents, and upload the data into Local DB.<br>
The output of "Succeeded uploading" means that data was uploaded into Local DB successfully.<br>

!!! Note
    Make sure the [log file](../config/scan-log.md) exists in the specified directory.<br>
    If the file does not exist or unreadable as a JSON file, dbAccessor returns error.<br>
    If you get an error, follow [FAQ for dbAccessor](../faq/accessor.md#not-found-xxx) to resolve it.

!!! Warning
    If the file is unreadable or unsuitable to upload, dbAccessor returns error.<br>
    If you get an error, follow [FAQ for dbAccessor](../faq/accessor.md#could-not-parse-xxx) to resolve it.<br>

#### Upload QC Scan Data

```bash
$./bin/dbAccessor -S data/last_scan/ -Q
[  info  ]: DBHandler: Register Scan Data
[  info  ]: ------------------------------
[  info  ]: Function: Upload scan data from specified directory
[  info  ]: Cache Directory: /home/example/YARR/data/006191_std_digitalscan
[  info  ]: -> Setting user config: /home/example/.yarr/localdb/user.json
[  info  ]: -> Setting site config: /home/example/.yarr/localdb/localhost_site.json
[  info  ]: -> Setting database config: /home/example/.yarr/localdb/localhost_database.json (default)
[  info  ]: Checking connection to DB Server: mongodb://127.0.0.1:27017/localdb ...
[  info  ]: ---> Good connection!
[  info  ]: Loading user information ...
[  info  ]: ~~~ {
[  info  ]: ~~~     ...
[  info  ]: ~~~ }
[  info  ]: Loading site information ...
[  info  ]: ~~~ {
[  info  ]: ~~~     ...
[  info  ]: ~~~ }
[  info  ]: Loading component information ...
[  info  ]: ~~~ {
[  info  ]: ~~~     ...
[  info  ]: ~~~ }
[  info  ]: Succeeded uploading scan data from /home/example/PhD/db/YARR/data/006191_std_digitalscan
[  info  ]: ------------------------------
```

In QC mode, the output and process are basically the same as the normal usage,
but some steps are added to check whether data (component, user, site information) is correct or missing.<br>

!!! Warning
    Data that does not meet the requirements will not be uploaded and an error will occur.<br>
    If you get an error, follow [FAQ for dbAccessor](../faq/accessor.md#not-found-xxx-data) to resolve it.

#### Interactive Mode

```bash
$ ./bin/dbAccessor -S data/last_scan/ -I
[  info  ]: DBHandler: Register Scan Data
[  info  ]: ------------------------------
[  info  ]: Function: Upload scan data from specified directory
[  info  ]: Cache Directory: /home/example/YARR/data/006191_std_digitalscan
[  info  ]: -> Setting user config: /home/example/.yarr/localdb/user.json
[  info  ]: -> Setting site config: /home/example/.yarr/localdb/localhost_site.json
[  info  ]: -> Setting database config: /home/example/.yarr/localdb/localhost_database.json (default)
[  info  ]: Checking connection to DB Server: mongodb://127.0.0.1:27017/localdb ...
[  info  ]: ---> Good connection!
[  info  ]: Loading user information ...
[  info  ]: ~~~ {
[  info  ]: ~~~     ...
[  info  ]: ~~~ }
[  info  ]: Loading site information ...
[  info  ]: ~~~ {
[  info  ]: ~~~     ...
[  info  ]: ~~~ }
[  info  ]: Loading component information ...
[  info  ]: ~~~ {
[  info  ]: ~~~     ...
[  info  ]: ~~~ }
[warning ]: -> Confirmation
[warning ]: Is this ok to upload data into Local DB?
[warning ]: (Please answer Y/y to continue or N/n to exit.)
[y/n]: y
```

In interactive mode, you can check data to upload and select whether to proceed.<br>

```bash
[  info  ]: Succeeded uploading scan data from /home/example/YARR/data/006191_std_digitalscan
[  info  ]: ------------------------------
```

The output and process are the same as the normal usage,
or the same as QC mode when used with the option **-Q**.
