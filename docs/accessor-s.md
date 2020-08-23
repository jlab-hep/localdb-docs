## dbAccessor -S

Contents:

1. [Synopsis](#1-synopsis)
2. [Installation](#2-installation)
3. [Syntax](#3-syntax)
4. [Examples](#4-examples)
5. [FAQ](#5-faq)

### 1. Synopsis

You can upload scan data from the specified scan result directory into Local DB by [dbAccessor -S](accessor-s.md)

### 2. Installation

The DB Accessor is included as part of [YARR SW](https://yarr.readthedocs.io/en/latest/).<br>
Follow the [dbAccessor Guide](accessor.md) to setup the command.

### 3. Syntax

The [dbAccessor -S](accessor-s.md) command has the following form:

```bash
$ ./bin/dbAccessor -S <path/to/result/dir>
                   [-d <path/to/database.json>]
                   [-Q]
                   [-I]
```

**Command Line Arguments**

- **``-S <path>``**<br>
Sets command to upload scan data and specifies the path to scan result directory to upload.<br>
Make sure the [scanLog.json](scan-log.md) exists in the specified directory.

**Additional options**

- **``-d <path>``**<br>
Specifies the path to [database config file](database-config.md).<br>
If -d is not specified, dbAccessor sets the path of "dbCfg" written in [scanLog.json](scan-log.md) located in the specified scan result directory,<br>
or sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](database-config.md) if no "dbCfg" written in [scanLog.json](scan-log.md).
- **``-Q``**<br>
Sets QC mode and add a step to check if the data to upload is suitable for QC.
- **``-I``**<br>
Sets interactive mode and add a step to ask the user to check the data to upload interactively.

### 4. Examples

#### Normal Usage

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

The dbAccessor loads files in the specified result directory while displaying the contents, and upload the data into Local DB.<br>


but in the QC mode, some steps are added to check whether data (component, user, site information) is correct or missing,<br>
data that does not meet the requirements will not be uploaded and an error will occur.<br>
If you get an error, follow [FAQ for dbAccessor](accessor-faq.md) to resolve it.


If the file is unreadable or unsuitable to upload,




The output of "Succeeded uploading" means that data was uploaded into Local DB successfully.<br>
Make sure the [log file](scan-log.md) exists in the specified directory.<br>
If the file does not exist or unreadable as a JSON file, dbAccessor returns error.<br>
If you get an error, follow [FAQ for dbAccessor](accessor-faq.md) to resolve it.

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

The output and process are basically the same as the normau usage,<br>
but in the QC mode, some steps are added to check whether data (component, user, site information) is correct or missing,<br>
data that does not meet the requirements will not be uploaded and an error will occur.<br>
If you get an error, follow [FAQ for dbAccessor](accessor-faq.md) to resolve it.

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
[  info  ]: Succeeded uploading scan data from /home/example/YARR/data/006191_std_digitalscan
[  info  ]: ------------------------------
```

### 5. FAQ



