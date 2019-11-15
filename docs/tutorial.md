# Quick Tutorial

You can store result data by YARR immediately following the tutorial.<br>

### Upload

You can scan and upload the test data into Local DB by `scanConsole -W`. <br>
First please prepare config files following [this sample format](https://localdb-docs.readthedocs.io/en/master/config/#user-cfg) and provide them with option '-u <user config file>' and '-i <site config file>', <br>
or ${USERNAME} and ${HOSTNAME} will be stored as default infromation.

```bash
$ ./bin/scanConsole \
-r configs/controller/emuCfg.json \
-c configs/connectivity/example_fei4b_setup.json \
-s configs/scans/fei4/std_digitalscan.json \
-W \
-u user.json \
-i site.json
<lots of text>
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# Local DB Server: mongodb://127.0.0.1:27017
#DB INFO# ---> connection is good.
#DB INFO# -----------------------
#DB INFO# Uploading in the back ground. (log: ~/.yarr/localdb/log/)
```
> [Advanced tutorial for scanConsole -W](https://localdb-docs.readthedocs.io/en/master/upload/#upload-test-data)

You can check if the upload is success in log file `${HOME}/.yarr/localdb/log/${day}.log`:

```log
2019-08-01 10:55:46,821 - INFO: -----------------------
2019-08-01 10:55:46,821 - INFO: Function: Upload Scan Data
2019-08-01 10:55:46,823 - INFO: Local DB Server: mongodb://127.0.0.1:27017
2019-08-01 10:55:46,826 - INFO: ---> connection is good.
2019-08-01 10:55:46,826 - INFO: Cache Directory: /home/akubata/work/YARR/data/000186_std_digitalscan/
2019-08-01 10:55:47,058 - INFO: Success
2019-08-01 10:55:47,060 - INFO: -----------------------
```
> [More detail about another upload functions](https://localdb-docs.readthedocs.io/en/master/upload/)

### Retrieve

You can check the uploaded test data log by `localdbtool-retrieve log`:

```bash
$ ./localdb/bin/localdbtool-retrieve log
#DB INFO# -----------------------
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017
#DB INFO#    The connection is GOOD.
test data ID: 5d8da5eda45ae057dbd1fbd6
User      : user at site
Date      : 2019/09/27 15:02:17
Chip      : JohnDoe_0
Run Number: 5635
Test Type : std_digitalscan
DCS Data  : NULL
# Ctrl+C can terminate the output test log
```
> [Advanced tutorial for Retrieve Tool](https://localdb-docs.readthedocs.io/en/master/retrieve/)

You can retrieve the uploaded data into the local directory by `localdbtool-retrieve pull`:

```bash
$ ./localdb/bin/localdbtool-retrieve pull
#DB INFO# -----------------------
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017
#DB INFO#    The connection is GOOD.
#DB INFO# test data ID: 5d8da5eda45ae057dbd1fbd6
#DB INFO# - User      : user at site
#DB INFO# - Date      : 2019/09/27 15:02:17
#DB INFO# - Chips     : JohnDoe_0
#DB INFO# - Run Number: 5635
#DB INFO# - Test Type : std_digitalscan
#DB INFO# Retrieve ... ./db-data/ctrlCfg.json
#DB INFO# Retrieve ... ./db-data/dbCfg.json
#DB INFO# Retrieve ... ./db-data/siteCfg.json
#DB INFO# Retrieve ... ./db-data/userCfg.json
#DB INFO# Retrieve ... ./db-data/std_digitalscan.json
#DB INFO# Retrieve ... ./db-data/scanLog.json
#DB INFO# Retrieve ... ./db-data/JohnDoe_0_EnMask.dat
#DB INFO# Retrieve ... ./db-data/JohnDoe_0_OccupancyMap.dat
#DB INFO# Retrieve ... ./db-data/JohnDoe_0_beforeCfg.json
#DB INFO# Retrieve ... ./db-data/fei4b_test.json
#DB INFO# Retrieve ... ./db-data/JohnDoe_0_afterCfg.json
#DB INFO# Retrieve ... ./db-data/connectivity.json
#DB INFO# -----------------------
```
> [Advanced tutorial for Retrieve Tool](https://localdb-docs.readthedocs.io/en/master/retrieve/)

* List of restored data (default dir: `YARR/db_data`)
    * Test Information (Data ID, User, Date, Chips, Run #, Test type)
    * connectivity config file
    * controller config file
    * scan config file
    * chip config file (original/before/after)
    * result data file
    * database config file
    * user config file
    * site config file

### Register Component

You can register the component data and upload test data associated with the registered component data.<br>
First please prepare connectivity file following [this sample format](https://localdb-docs.readthedocs.io/en/master/config/#component-cfg) and register by `dbAccessor -C -c <component connectivity file> -u <user config file> -i <site config file>`:<br>

```bash
$ cd YARR
$ ./bin/dbAccessor -C -c component.json -u user.json -i site.json
<some texts>
Do you continue to upload data into Local DB? [y/n]
y

#DB INFO# Completed the upload successfuly.
#DB INFO# -----------------------
```
> [More detail about Component Registration](https://localdb-docs.readthedocs.io/en/master/upload/#register-chipmodule-data)

After registration, you can retrieve/generate the connectivity config file and the chip config files by `localdb-retrieve pull --chip <SERIAL NUMBER>`.<br>

```bash
$ ./localdb/bin/localdb-retrieve pull --chip <SERIAL NUMBER>
#DB INFO# -----------------------
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017/localdb
#DB INFO# ---> Connection is GOOD.
#DB WARNING# Not found test data of the component: <SERIAL NUMBER>
#DB INFO# component data ID: 5dce77c414dc504d3ad53e80
#DB INFO# - Name: <SERIAL NUMBER>  Type: RD53A
#DB INFO# Retrieve ... ./db-data/<SERIAL NUMBER>.json
#DB INFO# Retrieve ... ./db-data/connectivity.json
#DB INFO# -----------------------
```
> [More detail about retrieving funtion](https://localdb-docs.readthedocs.io/en/master/retrieve/)

And you can upload test data associated with component data using these config files by `scanConsole`.

```bash
$ ./bin/scanConsole \
-r configs/controller/emuCfg.json \
-c db-data/<SERIAL NUMBER>.json \
-s configs/scans/fei4/std_digitalscan.json \
-W \
-u user.json \
-i site.json
<lots of text>
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# Local DB Server: mongodb://127.0.0.1:27017
#DB INFO# ---> connection is good.
#DB INFO# -----------------------
#DB INFO# Uploading in the back ground. (log: ~/.yarr/localdb/log/)
```
> [Advanced tutorial for Component Registration](https://localdb-docs.readthedocs.io/en/master/upload/#register-chipmodule-data)

### Local DB Tools

You can handle data in Local DB using Local DB Tools:

* [Viewer Application](#viewer-application)
* [Synchronization Tool](#sync-tool)
* [Archive Tool](#archive-tool)

```bash
$ git clone https://gitlab.cern.ch/YARR/localdb-tools.git
```

#### Viewer Application

```bash
# 1. Set Application
$ cd localdb-tools/viewer
$ ./setup_viewer.sh

# 2. Run Application
$ ./app.py --config conf.yml &
# ---> Access 'http://127.0.0.1:5000/localdb/' or
#      'http://IPaddress/localdb/' on browser to check data in Local DB
```
> [Advanced tutorial for Viewer Application](https://localdb-docs.readthedocs.io/en/master/viewer/)

#### Synchronization Tool

```bash
# 1. Set Tool
$ cd localdb-tools/sync-tool
$ ./setup_sync_tool.sh

# 2. Run Tool
$ ./bin/localdbtool-sync.py --sync-opt <option> --config my_configure.yml
```
> [Advanced tutorial for Synchronization Tool](https://localdb-docs.readthedocs.io/en/master/sync/)

#### Archive Tool

```bash
# 1. Set Tool
$ cd localDB-tools/archive-tool
$ ./setup_archive_tool.sh

# 2. Run Tool
$ ./bin/localdbtool-archive.sh --config my_archive_configure.yml
```
> [Advanced tutorial for Archive Tools](https://localdb-docs.readthedocs.io/en/master/archive/)

