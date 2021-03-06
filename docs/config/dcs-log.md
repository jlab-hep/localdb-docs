# DCS Log File

The [dbAccessor](../tool/accessor.md) outputs the log file of the DCS uploading in the result directory when executing.<br>
You can specify the log file of the scan to upload data into Local DB.

#### File Format

The log file (usualy named "dbDcsLog.json") use the JSON format:

```json
{
    "dbCfg": {
        "KeyFile": "null",
        "auth": "default",
        "dbName": "localdb",
        "environment": ["vddd_voltage", "vddd_current", "vdda_voltage", "vdda_current", "vddcom_voltage", "vddcom_current", "hv_voltage", "hv_current", "temperature"],
        "hostIp": "127.0.0.1",
        "hostPort": "27017",
    },
    "environments": [{
            "chip": null,
            "description": "Parent VDDD Voltage [V]",
            "key": "vddd_voltage",
            "num": 0,
            "path": "/home/YARR/data/006233_std_digitalscan/vddd_voltage_0.dat",
            "status": "enabled"
        }],
    "siteCfg": {
        "code": "TITECH",
        "institution": "Tokyo Institute of Technology"
    },
    "startTime": 1598518435,
    "timestamp": "2020-08-27_17:53:55",
    "userCfg": {
        "description": "viewer",
        "institution": "CERN",
        "userName": "Test User",
        "viewerUser": "testuser"
    }
}
```

#### Core Options

!!! Danger
    Generally, the log file is automatically generated by the [dbAccessor](../tool/accessor.md)),
    so you do not need to prepare or rewrite it yourself.<br>
    But if you want to change the log, you must rewrite it properly, being careful of mistakes and data loss.

- `timestamp`<br>
_Type_ : string<br>
Timestamp written in the format "yyyy-MM-dd_HH:mm:ss" when the scan was executed.

- `startTime`<br>
_Type_ : int<br>
Timestamp written in the Unixtime when the scan started.

- `dbCfg`<br>
_Type_ : dictionary <br>
The contents of the [database config file](database.md).

- `userCfg`<br>
_Type_ : dictionary <br>
The contents of the [user config file](user.md).

- `siteCfg`<br>
_Type_ : dictionary <br>
The contents of the [site config file](site.md).

- `environments`<br>
_Type_ : list <br>
The contents of the [DCS config file](dcs.md).

