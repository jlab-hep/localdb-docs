# dbAccessor -F

### Table of Contents

1. [Synopsis](#1-synopsis)
2. [Installation](#2-installation)
3. [Syntax](#3-syntax)
4. [Examples](#4-examples)
5. [FAQ](#5-faq)

## 1. Synopsis

You can retrieve DCS data from influxDB and registered it into Local DB by [dbAccessor -F](f.md)

## 2. Installation

The DB Accessor is included as part of [YARR SW](http://yarr.web.cern.ch/yarr/).<br>
Follow the [dbAccessor Guide](../accessor.md) to setup the command.

## 3. Syntax

The [dbAccessor -F](f.md) command has the following form:

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
Sets command to upload DCS data from influxDB and specifies the path to [influxDB config file](../config/dcs.md#influxdb-config-file) to upload.
- **``-n <name>``**<db>
Specifies the component name to link the DCS data.
- **``-s <path>``**<br>
Specifies the path to [scan log file](../config/scan-log.md) of the scan result data to link the DCS data.

**Additional options**

- **``-d <path>``**<br>
Specifies the path to [database config file](../config/database.md).<br>
If -d is not specified, dbAccessor sets the path of "dbCfg" written in [scanLog.json](../config/scan-log.md) located in the specified scan result directory,<br>
or sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](../config/database.md) if no "dbCfg" written in [scanLog.json](../config/scan-log.md).<br>
Make sure the specified configuration is the same as when the scan data was registered.<br>
(The one written in [scanLog.json](../config/scan-log.md) should be match, so no need to specify anything usually.)
- **``-u <path>``**<br>
Specifies the path to [user config file](../config/user.md)<br>
If -u is not specified, dbAccessor sets the path of "userCfg" written in [scanLog.json](../config/scan-log.md) located in the specified scan result directory,<br>
or sets `HOME/.yarr/localdb/user.json` as [user config file](../config/user.md) if no "userCfg" written in [scanLog.json](../config/scan-log.md).<br>
Make sure the specified configuration is the same as when the scan data was registered.<br>
(The one written in [scanLog.json](../config/scan-log.md) should be match, so no need to specify anything usually.)
- **``-i <path>``**<br>
Specifies the path to [site config file](../config/site.md)<br>
If -i is not specified, dbAccessor sets the path of "siteCfg" written in [scanLog.json](../config/scan-log.md) located in the specified scan result directory,<br>
or sets `HOME/.yarr/localdb/HOSTNAME_site.json` as [site config file](../config/site.md) if no "siteCfg" written in [scanLog.json](../config/scan-log.md).<br>
Make sure the specified configuration is the same as when the scan data was registered.<br>
(The one written in [scanLog.json](../config/scan-log.md) should be match, so no need to specify anything usually.)
- **``-Q``**<br>
Sets QC mode and add a step to check if the data to upload is suitable for QC.
- **``-I``**<br>
Sets interactive mode and add a step to ask the user to check the data to upload interactively.

### 4. Examples

in edit
