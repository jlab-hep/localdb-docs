# DCS Tutorial

This tutorial describes the basic operations of DCS uploading.

!!! Warning
    If you do not have [YARR git repository](https://gitlab.cern.ch/YARR/YARR) or [Local DB Tools git retpository](https://gitlab.cern.ch/YARR/localdb-tools), or system packages required for those repositories, see the [installation guide](../installation.md) to install the missing ones.

### Table of Contents

1. [How to Upload DCS from Data File](#1-how-to-upload-dcs-from-data-file)
2. [How to Upload DCS from influxDB](#2-how-to-upload-dcs-from-influxdb)
3. [How to Check DCS data in Console](#3-how-to-check-dcs-data-in-console)
4. [How to Check DCS data in Viewer Application](#4-how-to-check-dcs-data-in-viewer)

---

## 1. How to Upload DCS from Data File

#### Setup for YARR binary command

First make sure to prepare the [DCS data file (dcs.dat)](../config/dcs.md#dcs-data-file):

```dat
key unixtime vddd_voltage vddd_current vdda_voltage vdda_current
num null 0 0 1 1
2019-06-24_20:49:13 1561376953 10 20 0 0
2019-06-24_20:49:23 1561376963 11 21 0 0
2019-06-24_20:49:33 1561376973 12 22 0 0
```

Next set the [DCS config file (dcs.json)](../config/dcs.md#dcs-config):

```json
{
    "environments": [{
        "description": "VDDD Voltage [V]",
        "key": "vddd_voltage",
        "num": 0,
        "path": "dcs.dat",
        "status": "enabled"
    },{
        "description": "VDDD Current [A]",
        "key": "vddd_current",
        "num": 0,
        "path": "dcs.dat",
        "status": "enabled"
    }]
}
```

Then you can upload DCS data associated with specific scan result data into Local DB by [YARR/bin/dbAccessor](../tool/accessor.md):

```bash
$ ./bin/dbAccessor -E dcs.json -s data/last_scan/scanLog.json

<lots of text>
[  info  ]: Succeeded uploading dcs data from /home/work/YARR/data/000004_std_digitalscan
```

The output of "Succeeded uploading" means that data was uploaded into Local DB successfully.<br>

## 2. How to Upload DCS from influxDB

in edit.

## 3. How to Check DCS Data in Console

Run [YARR/bin/dbAccessor](../tool/accessor.md) to check if the DCS data has been uploaded:

```bash
$ ./bin/dbAccessor -L
[  info  ]: DBHandler: Retrieve Test Log
[  info  ]: -----------------------
test data ID: 5f51e1343a4726a2fa828861
User      : dbadmin at localdb.server
Date      : 2020/09/04 15:18:32
Component : JohnDoe_0
Run Number: 11
Test Type : std_digitalscan
DCS Data  :
   vddd_voltage, vddd_current (JohnDoe_0)

test data ID: 5f51b7019e7ba2ff440ee06b
User      : dbadmin at localdb.server
Date      : 2020/09/04 11:45:51
Component : JohnDoe_0, DisabledChip_1
Run Number: 8
Test Type : std_digitalscan
DCS Data  :
   vddd_voltage, vddd_current (JohnDoe_0)
   vddd_voltage, vddd_current (DisabledChip_1)
### Ctrl+C can terminate the output test log
```

## 4. How to Check DCS Data in Viewer

in edit.
