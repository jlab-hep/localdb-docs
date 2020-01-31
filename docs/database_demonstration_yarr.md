# YARR

## Goal

Run the emulator for FE-I4B and upload the test results into Local DB ([MongoDB](database_demonstration_mongodb.md)).

## Getting start

### 1. Run the Emulator

Just type the following command to run the emulator.

```bash
$ cd ../
### pwd ---> path/to/YARR
$ ./bin/scanConsole \
-c configs/connectivity/example_fei4b_setup.json \
-r configs/controller/emuCfg.json \
-s configs/scans/fei4/std_digitalscan.json \
-p
<some texts>
Finishing run: 5840
./data/last_scan/JohnDoe_EnMask.png
./data/last_scan/JohnDoe_L1Dist.pdf
./data/last_scan/JohnDoe_OccupancyMap.png
```

You can check some plots in 'data/last_scan'

### Create ssh tunnel
```bash
$ ssh -2 -C -Y -L 27017:localhost:27107 {DB server IP} -fN
```


### 2. Set up database config
```bash
$ cd YARR
$ ./localdb/setup_db.sh
...
```

### 3. Login for the database 
```bash
$ cd YARR
$ ./localdb/login_mongodb.sh
...
```

### 4. Run the emulator with uploading to Local DB
<!--
First you have to prepare the config file for Local DB by 'setup_db.sh'<br>
In this step, you have to set the editor command (e.g. vim, emacs) if the environmental variable 'EDITOR' has not registered.

```bash
$ cd ../
$ cd localdb
$ ./setup_db.sh
<some steps>
[LDB] More detail:
[LDB]   Access 'https://localdb-docs.readthedocs.io/en/master/'
```
-->

```bash
$ ./localdb/bin/localdbtool-upload init
```

Run the emulator with option '-W' to upload the test data into Local DB.

```bash
$ ./bin/scanConsole \
-c configs/connectivity/example_fei4b_setup.json \
-r configs/controller/emuCfg.json \
-s configs/scans/fei4/std_digitalscan.json \
-W
<some texts>
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017/localdb
#DB INFO# ---> Connection is GOOD.
#DB INFO# -----------------------
#DB INFO# Uploading in the back ground. (log: ~/.yarr/localdb/log/)
```

You can the upload status in the log file '~/.yarr/localdb/log/DAY.log'.<br>
You can also check the data by accessing to http://{IP Address of DB machine}:5000/localdb/ on the machine's browser.<br>
Check [here](database_demonstration_viewer.md) to go to the steps for checking the Viewer Application.

Finish!

## More Detail

Check [YARR Docs](https://yarr.readthedocs.io/en/latest/) for more detail.
