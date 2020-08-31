# dbAccessor -E

### Table of Contents

1. [Synopsis](#1-synopsis)
2. [Installation](#2-installation)
3. [Syntax](#3-syntax)
4. [Examples](#4-examples)

## 1. Synopsis

You can upload DCS data according to the specified DCS configuration file into Local DB.

## 2. Installation

The DB Accessor is included as part of [YARR SW](http://yarr.web.cern.ch/yarr/).<br>
Follow the [dbAccessor Guide](../accessor.md) to setup the command.

## 3. Syntax

The [dbAccessor -E](e.md) command has the following form:

```bash
$ ./bin/dbAccessor -E <path/to/dcs.json>
                   -s <path/to/scanLog.json>
                   [-d <path/to/database.json>]
                   [-Q]
                   [-I]
```

###### Command Line Arguments

- **``-E <path>``**<br>
Sets command to upload DCS data and specifies the path to [DCS config file](../../config/dcs.md) to upload.
- **``-s <path>``**<br>
Specifies the path to [scan log file](../../config/scan-log.md) of the scan result data to link the DCS data.

###### Additional options

- **``-d <path>``**<br>
Specifies the path to [database config file](../../config/database.md).<br>
If -d is not specified, dbAccessor sets the path of "dbCfg" written in [scanLog.json](../../config/scan-log.md) located in the specified scan result directory,
or sets `HOME/.yarr/localdb/HOSTNAME_database.json` as [database config file](../../config/database.md) if no "dbCfg" written in [scanLog.json](../../config/scan-log.md).<br>
Make sure the specified configuration is the same as when the scan data was registered.<br>
- **``-Q``**<br>
Sets QC mode and add a step to check if the data to upload is suitable for QC.
- **``-I``**<br>
Sets interactive mode and add a step to ask the user to check the data to upload interactively.

## 4. Examples

#### Normal Usage

You can upload the DCS data after uploading the scan result to link.<br>
Make sure the scan result is uploaded by [dbAccessor -L](l.md) command:

```bash
$./bin/dbAccessor -L
[  info  ]: DBHandler: Retrieve Test Log
[  info  ]: -----------------------
[  info  ]: Checking connection to DB Server: mongodb://127.0.0.1:27017/localdb ...
[  info  ]: ---> Good connection!

test data ID: 5f45ff5d012e42929345941d
User      : user at site
Date      : 2020/08/26 15:20:53
Component : JohnDoe_0
Run Number: 6219
Test Type : std_digitalscan
DCS Data  : NULL
```

If you can confirm the scan data is uploaded and DCS data is **NULL**,
you can upload DCS data associated with the scan data.<br>
Here, let's upload VDDD voltage data as an example.

```json
{
    "environments": [{
        "description": "Parent VDDD Voltage [V]",
        "key": "vddd_voltage",
        "num": 0,
        "path": "dcs.dat",
        "status": "enabled"
    }]
}
```

First, prepare a [DCS config file named **dcs.json**](../../config/dcs.md#dcs-config-file).<br>

```dat
key unixtime vddd_voltage vddd_current vdda_voltage vdda_current
num null 0 0 0 0
2019-06-24_20:49:13 1561376953 10 20 0 0
2019-06-24_20:49:23 1561376963 11 21 0 0
2019-06-24_20:49:33 1561376973 12 22 0 0
```

Make sure the [data file named **dcs.dat**](../../config/dcs.md#dcs-dat-file) specified by "path" in the [DCS config file](../../config/dcs.md#dcs-config-file) exists, its contents follow the notation of [DCS data file](../../config/dcs.md#dcs-dat-file), and the DCS data specified by the "key" and "num" in the [DCS config file](../../config/dcs.md#dcs-config-file) is written.<br>

The combination of "key" (**vddd_voltage**) and "num" (**0**) specified in the [DCS config file](../../config/dcs.md#dcs-config-file) are used to specify the DCS data in the [data file](../../config/dcs.md#dcs-dat-file).<br>
All data in the column with the specified key in the first row and the specified number in the second row is regarded as DCS data and uploaded into Local DB along with the unixtime, so in this case, <br>
```json
[
    { Unixtime: 1561376953, Value: 10 },
    { Unixtime: 1561376963, Value: 11 },
    { Unixtime: 1561376973, Value: 12 }
]
```
will be uploaded into Local DB.

You can link the DCS data to the scan data and upload it into Local DB by specifying the scan data with the [scanLog.json](../../config/scan-log.md):

```bash
$ ./bin/dbAccessor -E dcs.json -s data/last_scan/scanLog.json
[  info  ]: DBHandler: Register Environment Data
[  info  ]: ------------------------------
[  info  ]: Function: Upload DCS data from specified directory
[  info  ]: Cache Directory: /home/example/YARR/data/006219_std_digitalscan
[  info  ]: Checking connection to DB Server: mongodb://127.0.0.1:27017/localdb ...
[  info  ]: ---> Good connection!
[  info  ]: -> Setting DCS Log dbDcsLog.json
[  info  ]: Loading DCS information ...
[  info  ]: ~~~ {
[  info  ]: ~~~     ...
[  info  ]: ~~~ }
[  info  ]: Succeeded uploading dcs data from /home/example/YARR/data/006219_std_digitalscan
[  info  ]: ------------------------------
```

The dbAccessor loads the DCS config and data files while displaying the contents, and upload the data into Local DB.<br>
The output of "Succeeded uploading" means that data was uploaded into Local DB successfully.<br>
You can check if the data was uploaded by:

```bash
$ ./bin/dbAccessor -L
[  info  ]: DBHandler: Retrieve Test Log
[  info  ]: -----------------------
[  info  ]: Checking connection to DB Server: mongodb://127.0.0.1:27017/localdb ...
[  info  ]: ---> Good connection!

test data ID: 5f45ff5d012e42929345941d
User      : user at site
Date      : 2020/08/26 15:20:53
Component : JohnDoe_0
Run Number: 6220
Test Type : std_digitalscan
DCS Data  :
   vddd_voltage (JohnDoe_0)
```

!!! Warning
    If the specified scan data has not been uploaded to the Local DB, an error will occur.<br>
    If you get an error, follow [how to deal with error in dbAccessor](../../error/accessor.md#not-found-xxx-data) to resolve it.
