# Scan the component data

## Goal

Run scanConsole with the component data and upload the results into Local DB.

## 0. Login LocalDB

```bash
$ cd YARR
$ source localdb/login_mongodb.sh
...
```

## 1. Create connectivity config for the module

Please be sure to register module and chip data in Local DB using [Viewer Application](database_demonstration_check_viewer.md) before creating config.<br>
**This function is not available in YARR v1.1.0.**<br>
**Please change to the devel branch if want to use.**<br>

```bash
$ cd YARR
$ ./localdb/bin/localdbtools-retrieve pull --chip 20UPGRS0000009 
<some of text>
```

The config files for the module are generated in './db-data'.<br>

## 2. scanConsole

Please be sure if there are any mistakes in the config files in './db-data'.

```bash
$ cd YARR
$ ./bin/scanConsole \
-r configs/controller/emuCfg.json \
-c db-data/connectivity.json \
-s configs/scans/fei4/std_digitalscan.json \
-W
<lots of text>
```

## 3. Check

Check if the test data was uploaded following [this page](database_demonstration_check_viewer.md).<br>

## 4. DCS Upload

First prepare the DCS config file (localdb/configs/influxdb_connectivity.json) as follows:

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
$ ./bin/dbAccessor \
-F influxdb-connectivity.json \
-n 20UPGRA0000026 \
-s ./data/last_scan/scanLog.json
```

## 5. Check

Check if the test data was uploaded following [http://127.0.0.1:5000/localdb/scan](http://127.0.0.1:5000/localdb/scan).<br>

## 6. Tuning

```bash
1. std_digitalscan
2. diff_analogscan
3. diff_thresholdscan
4. diff_tune_globalthreshold
5. diff_tune_pixelthreshold
6. diff_retune_pixelthreshold
7. diff_tune_finepixelthreshold
8. diff_totscan
9. diff_noisescan
```

Finish!
