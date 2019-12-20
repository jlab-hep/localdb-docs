# Scan the component data

## Goal

Run scanConsole with the component data and upload the results into Local DB.

## 1. Create connectivity config for the module

Please be sure to register module and chip data in Local DB using [Viewer Application](database_demonstration_check_viewer.md) before creating config.<br>
**This function is not available in YARR v1.1.0.**<br>
**Please change to the devel branch if want to use.**<br>

```bash
$ cd YARR
$ ./localdb/bin/localdb-retrieve pull --chip <ATLAS SERIAL NUMBER>
<some of text>
```

The config files for the module are generated in './db-data'.<br>

## 2. scanConsole

Please be sure if there are any mistakes in the config files in './db-data'.

```bash
$ cd YARR
$ ./bin/scanConsole \
-r configs/controller/emuCfg.json \
-c db-data/<ATLAS SERIAL NUMBER>.json \
-s configs/scans/fei4/std_digitalscan.json \
-W
<lots of text>
```

## 3. Check

Check if the test data was uploaded following [this page](database_demonstration_check_viewer.md).<br>

## 4. DCS Upload

First prepare the DCS config file (e.g. influxdb-connectivity.json) as follows:

```json
{
    "measurement": "dummy_thermal",
    "dcsList": [{
        "key": "temperature",
        "data_name": "temperature_1",
        "data_unit": "temperature_1_unit",
        "description": "Room Temperature [C]",
        "setting": 28
    },{
        "key": "temperature",
        "data_name": "temperature_2",
        "data_unit": "temperature_2_unit",
        "description": "Board Temperature [C]",
        "setting": 28
    }]
}
```

Next run dbAccessor:

```bash
$ ./bin/dbAccessor \
-F influxdb-connectivity.json \
-n <ATLAS SERIAL NUMBER> \
-s ./data/last_scan/scanLog.json
```

## 5. Check

Check if the test data was uploaded following [this page](database_demonstration_check_viewer.md).<br>

Finish!
