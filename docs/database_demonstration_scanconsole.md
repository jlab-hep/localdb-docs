# Scan the component data

## Goal

Run scanConsole with the component data and upload the results into Local DB.

### 1.Create ssh tunnel
```bash
$ ssh -2 -C -Y -L 27017:localhost:27017 root@localdbserverX -fN -p22
Password:
$
```


### 2. Set up database config
```bash
$ cd ~/work/YARR
$ ./localdb/setup_db.sh
...
```

### 3. Login for the database 
```bash
$ source localdb/login_mongodb.sh
...
```

```bash
$ ./localdb/bin/localdbtools-retrieve pull --chip 20UPGRS0000009 
<some of text>
```

The config files for the module are generated in './db-data'.<br>

### 4. Change stage name 

Change the module config file (path is db-data/connectivity.json) as follows:


### 5. scanConsole and combine DCS data

```bash
$ ./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/std_digitalscan.json -W
<lots of text>
```
Firstly change the DCS config file (path is localdb/configs/influxdb_connectivity.json) as follows:

```json
{
    "environments" : [
        {
            "measurement" : "Temperature",
            "dcsList" : [
                {
                    "key"        : "temperature",
                    "data_name"  : "temp1",
                    "data_unit"  : "temp1_unit",
                    "description": "Room Temperature [C]",
                    "setting"    : 28
                },{
                    "key"        : "temperature",
                    "data_name"  : "temp2",
                    "data_unit"  : "temp2_unit",
                    "description": "Board Temperature [C]",
                    "setting"    : 28
                }
            ]
        },{
            "measurement" : "LV"
            "dcsList" : [
                {
                    "key"        : "vddd_voltage",
                    "data_name"  : "LV_Voltage",
                    "data_unit"  : "LV_Voltage_unit",
                    "description": "VDDD Voltage [V]",
                    "setting"    : 1.75
                },
                {
                    "key"        : "vdda_current",
                    "data_name"  : "LV_Current",
                    "data_unit"  : "LV_Current_unit",
                    "description": "VDDD Current [A]",
                    "setting"    : 1.1
                }
            ]
        }
    ]
}
```

Next run dbAccessor:

```bash
$ ./bin/dbAccessor -F localdb/cobfigs/influxdb_connectivity.json -n 20UPGRA0000026 -s data/last_scan/scanLog.json
```
Check if the test data was uploaded following [http://127.0.0.1:5000/localdb/scan](http://127.0.0.1:5000/localdb/scan).<br>

### 6. scanConsole and combine DCS data

If you want to upload DCS data for each scan, you have to put the command between scans.(./bin/dbAccessor -F localdb/cobfigs/influxdb_connectivity.json -n 20UPGRA0000026 -s data/last_scan/scanLog.json)
```bash
$ ./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/std_digitalscan.json -W
$ ./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_analogscan.json -W
$ ./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_thresholdscan.json -W
$ ./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_tune_globalthreshold.json -W
$ ./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_tune_pixelthreshold.json -W
$ ./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_retune_pixelthreshold.json -W
$ ./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_tune_finepixelthreshold.json -W
$ ./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_totscan.json -W
$ ./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_noise.json -W
```
Check the test results [http://127.0.0.1:5000/localdb/scan](http://127.0.0.1:5000/localdb/scan).<br>

Finish!
