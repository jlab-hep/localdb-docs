# DB Accessor

The **DB Accessor** is to easy handle Local DB.<br>
You can upload local data to Local DB or download data locally from Local DB easily by using this command.

Contents:

1. [Command](#1-command)
2. [Getting Start](#2-getting-start)
3. [Usage](#3-usage)
    - a. [Check the connection to Local DB](#a-check-connection)
    - b. [Upload scan data from scan result directory into Local DB](#b-upload-scan-data)
    - c. [Upload DCS data from data files into Local DB](#c-upload-dcs-data)
    - d. [Upload DCS data from influxDB into Local DB](#d-upload-dcs-data-from-influxdb)
    - e. [Upload scan/DCS data recorded in cache into Local DB](#e-upload-cache-data)
    - f. [Retrieve scan data from Local DB](#f-retrieve-scan-data)
    - g. [Register non-QC componnet data into Local DB](#g-register-component-data)
4. [FAQ](#4-faq)

## 1. Command

- Location: ``YARR/bin/dbAccessor``
- Usage: ``dbAccessor <-command> [-option]``

```bash
$ cd YARR
$ ./bin/dbAccessor

#These are common DB commands used in verious situations:
#
#    -h                     Shows this.
#    -N                     Check the connection to Local DB.
#    -S <result dir>        Upload scan data from the specified scanresult directory into Local DB.
#    -E <dcs.json>          Upload DCS data according to the specified DCS config file into Local DB.
#       -s <scanLog.json>   Provide path to log file of scan result data to link the DCS data.
#    -F <influx.json>       Retrieve DCS data from influxDB and Upload the data according to the specified influxDB config file into Local DB.
#       -n <component name> Provide component name to link the DCS data.
#       -s <scanLog.json>   Provide path to log file of scan result data to link the DCS data.
#    -R                     Upload scan/DCS data recorded in the cache ($HOME/.yarr/localdb/run.dat or dcs.dat) into Local DB.
#    -D                     Retrieve data from Local DB. (Default. most recently saved data)
#       [-n <cmp name>]     Provide component (chip/module) name.
#       [-p <output dir>]   Provide path to directory to put config files. (Default. ./db-data)
#       [-c <cmp.json>]     Provide path to component connectivity config file to create chip config files.
#    -C                     Upload non-QC component data into Local DB.
#       -c <cmp.json>       Provide path to component connectivity config file to upload.
#
#optional arguments:
#    -Q                     Set QC mode (add a step to check if the data to upload is suitable for QC).
#    -I                     Set interactive mode (add a step to ask the user to check the data to upload interactively).
#    -d <database.json>     Provide path to database config file.
#    -u <user.json>         Provide path to user config file.
#    -i <site.json>         Provide path to site config file.
```

## 2. Getting start

#### 0. Install & Setup

The DB Accessor is included as part of [YARR SW](https://yarr.readthedocs.io/en/latest/).<br>
Follow the [installation tutorial](requirements.md) to install required packages and be sure to build YARR SW:

```bash
$ cd YARR
$ mkdir build && cd build
$ cmake3 ../
$ make -j4
```

And be sure to setup Local DB configuration files using [YARR/localdb/setup_db.sh](setup-db.md) shell:

```bash
$ cd YARR
$ ./localdb/setup_db.sh
```

#### 1. Confirmation

You can run the [DB Accessor](accessor.md) with command-line option **-N** to check if the command is working and the connection to Local DB is good:

```bash
$ ./bin/dbAccessor -N
```

## 3. Usage

You can use the DB accessor to do the following operation:

* a. [Check the connection to Local DB](#a-check-connection)
* b. [Upload scan data from scan result directory into Local DB](#b-upload-scan-data)
* c. [Upload DCS data from data files into Local DB](#c-upload-dcs-data)
* d. [Upload DCS data from influxDB into Local DB](#d-upload-dcs-data-from-influxdb)
* e. [Upload scan/DCS data recorded in cache into Local DB](#e-upload-cache-data)
* f. [Retrieve scan data from Local DB](#f-retrieve-scan-data)
* g. [Register non-QC componnet data into Local DB](#g-register-component-data)

### a. Check Connection

You can check if the command is working and the connection to Local DB is good by:

```bash
$ ./bin/dbAccessor -N
                   [-d <path/to/database.json>]
```

**Command Line Arguments**

- **``-N``**<br>
Sets command to check the connection to Local DB.

**Additional options**

- **``-d <path>``**<br>
Specifies the path to [database config file](config.md).<br>
If -d is not specified, dbAccessor sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](config.md).

### b. Upload Scan Data

You can upload scan data from the specified scan result directory into Local DB by:

```bash
$ ./bin/dbAccessor -S <path/to/result/dir>
                   [-d <path/to/database.json>]
                   [-Q]
                   [-I]
```

**Command Line Arguments**

- **``-S <path>``**<br>
Sets command to upload scan data and specifies the path to scan result directory to upload.<br>
Ensure the [scanLog.json](config.md) exists in the specified directory.

**Additional options**

- **``-d <path>``**<br>
Specifies the path to [database config file](config.md).<br>
If -d is not specified, dbAccessor sets the path of "dbCfg" written in [scanLog.json](config.md) located in the specified scan result directory,<br>
or sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](config.md) if no "dbCfg" written in [scanLog.json](config.md).
- **``-Q``**<br>
Sets QC mode and add a step to check if the data to upload is suitable for QC.
- **``-I``**<br>
Sets interactive mode and add a step to ask the user to check the data to upload interactively.

### c. Upload DCS Data

You can upload DCS data according to the specified DCS configuration file into Local DB by:

```bash
$ ./bin/dbAccessor -E <path/to/dcs.json>
                   -s <path/to/scanLog.json>
                   [-d <path/to/database.json>]
                   [-u <path/to/user.json>]
                   [-i <path/to/site.json>]
                   [-Q]
                   [-I]
```

**Command Line Arguments**

- **``-E <path>``**<br>
Sets command to upload DCS data and specifies the path to [DCS config file](config.md) to upload.
- **``-s <path>``**<br>
Specifies the path to [scan log file](config.md) of the scan result data to link the DCS data.

**Additional options**

- **``-d <path>``**<br>
Specifies the path to [database config file](config.md).<br>
If -d is not specified, dbAccessor sets the path of "dbCfg" written in [scanLog.json](config.md) located in the specified scan result directory,<br>
or sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](config.md) if no "dbCfg" written in [scanLog.json](config.md).<br>
Ensure the specified configuration is the same as when the scan data was registered.<br>
(The one written in [scanLog.json](config.md) should be match, so no need to specify anything usually.)
- **``-u <path>``**<br>
Specifies the path to [user config file](config.md)<br>
If -u is not specified, dbAccessor sets the path of "userCfg" written in [scanLog.json](config.md) located in the specified scan result directory,<br>
or sets `HOME/.yarr/localdb/user.json` as [user config file](config.md) if no "userCfg" written in [scanLog.json](config.md).<br>
Ensure the specified configuration is the same as when the scan data was registered.<br>
(The one written in [scanLog.json](config.md) should be match, so no need to specify anything usually.)
- **``-i <path>``**<br>
Specifies the path to [site config file](config.md)<br>
If -i is not specified, dbAccessor sets the path of "siteCfg" written in [scanLog.json](config.md) located in the specified scan result directory,<br>
or sets `HOME/.yarr/localdb/HOSTNAME_site.json` as [site config file](config.md) if no "siteCfg" written in [scanLog.json](config.md).<br>
Ensure the specified configuration is the same as when the scan data was registered.<br>
(The one written in [scanLog.json](config.md) should be match, so no need to specify anything usually.)
- **``-Q``**<br>
Sets QC mode and add a step to check if the data to upload is suitable for QC.
- **``-I``**<br>
Sets interactive mode and add a step to ask the user to check the data to upload interactively.

### d. Upload DCS Data from InfluxDB

You can retrieve DCS data from influxDB and registered it into Local DB by:

```bash
$ ./bin/dbAccessor -F <path/to/influx.json>
                   -n <component name>
                   -s <path/to/scanLog.json>
                   [-d <path/to/database.json>]
                   [-u <path/to/user.json>]
                   [-i <path/to/site.json>]
                   [-Q]
                   [-I]
```

**Command Line Arguments**

- **``-F <path>``**<br>
Sets command to upload DCS data from influxDB and specifies the path to [influxDB config file](config.md) to upload.
- **``-n <name>``**<br>
Specifies the component name to link the DCS data.
- **``-s <path>``**<br>
Specifies the path to [scan log file](config.md) of the scan result data to link the DCS data.

**Additional options**

- **``-d <path>``**<br>
Specifies the path to [database config file](config.md).<br>
If -d is not specified, dbAccessor sets the path of "dbCfg" written in [scanLog.json](config.md) located in the specified scan result directory,<br>
or sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](config.md) if no "dbCfg" written in [scanLog.json](config.md).<br>
Ensure the specified configuration is the same as when the scan data was registered.<br>
(The one written in [scanLog.json](config.md) should be match, so no need to specify anything usually.)
- **``-u <path>``**<br>
Specifies the path to [user config file](config.md)<br>
If -u is not specified, dbAccessor sets the path of "userCfg" written in [scanLog.json](config.md) located in the specified scan result directory,<br>
or sets `HOME/.yarr/localdb/user.json` as [user config file](config.md) if no "userCfg" written in [scanLog.json](config.md).<br>
Ensure the specified configuration is the same as when the scan data was registered.<br>
(The one written in [scanLog.json](config.md) should be match, so no need to specify anything usually.)
- **``-i <path>``**<br>
Specifies the path to [site config file](config.md)<br>
If -i is not specified, dbAccessor sets the path of "siteCfg" written in [scanLog.json](config.md) located in the specified scan result directory,<br>
or sets `HOME/.yarr/localdb/HOSTNAME_site.json` as [site config file](config.md) if no "siteCfg" written in [scanLog.json](config.md).<br>
Ensure the specified configuration is the same as when the scan data was registered.<br>
(The one written in [scanLog.json](config.md) should be match, so no need to specify anything usually.)
- **``-Q``**<br>
Sets QC mode and add a step to check if the data to upload is suitable for QC.
- **``-I``**<br>
Sets interactive mode and add a step to ask the user to check the data to upload interactively.

### e. Upload Cache Data

When you could not upload scan/DCS data because of the bad connection to Local DB server,<br>
the cache data and log file ([scanLog.json](config.md)/[dbDcsLog.json](config.md)) would be stored in the result directory, <br>
and the record is written to the file: `HOME/.yarr/run.dat`/`HOME/.yarr/dcs.dat`.

You can upload all cache data into Local DB when the good connection to Local DB server by:

```bash
$ ./bin/dbAccessor -R
                   [-d <path/to/database.json>]
                   [-u <path/to/user.json>]
                   [-i <path/to/site.json>]
                   [-Q]
                   [-I]
```

**Command Line Arguments**

- **``-R``**<br>
Sets command to upload cache data

**Additional options**

- **``-d <path>``**<br>
Specifies the path to [database config file](config.md).<br>
If -d is not specified, dbAccessor sets the path of "dbCfg" written in [scanLog.json](config.md) located in the specified scan result directory,<br>
or sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](config.md) if no "dbCfg" written in [scanLog.json](config.md).
- **``-u <path>``**<br>
Specifies the path to [user config file](config.md)<br>
If -u is not specified, dbAccessor sets the path of "userCfg" written in [scanLog.json](config.md) located in the specified scan result directory,<br>
or sets `HOME/.yarr/localdb/user.json` as [user config file](config.md) if no "userCfg" written in [scanLog.json](config.md).
- **``-i <path>``**<br>
Specifies the path to [site config file](config.md)<br>
If -i is not specified, dbAccessor sets the path of "siteCfg" written in [scanLog.json](config.md) located in the specified scan result directory,<br>
or sets `HOME/.yarr/localdb/HOSTNAME_site.json` as [site config file](config.md) if no "siteCfg" written in [scanLog.json](config.md).
- **``-Q``**<br>
Sets QC mode and add a step to check if the data to upload is suitable for QC.
- **``-I``**<br>
Sets interactive mode and add a step to ask the user to check the data to upload interactively.

### f. Retrieve Scan Data

You can retrieve scan data from Local DB by:

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
Specifies the path to [component connectivity config file](config.md).<br>
You can create chip config files with filling chip names and chip IDs <br>
according the specified connectivity config even if the chips are not registered in Local DB.
- **``-d <path>``**<br>
Specifies the path to [database config file](config.md).<br>
If -d is not specified, dbAccessor sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](config.md).

### g. Register Component Data

Basically component data is registered on ITk PD, and Local DB downloads and uses it.<br>
But if you want to manage non-QC component data, You can register component data by:

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
Specifies the path to [database config file](config.md).<br>
If -d is not specified, dbAccessor sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](config.md).
- **``-u <path>``**<br>
Specifies the path to [user config file](config.md)<br>
If -u is not specified, dbAccessor sets `HOME/.yarr/localdb/user.json` as [user config file](config.md).
- **``-i <path>``**<br>
Specifies the path to [site config file](config.md)<br>
If -i is not specified, dbAccessor sets `HOME/.yarr/localdb/HOSTNAME_site.json` as [site config file](config.md).

## 4. FAQ

in edit.

This is a quick summary of the major commands; the previous chapters explain how these work in more detail.

in edit.
