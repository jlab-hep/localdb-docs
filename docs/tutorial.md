# Quick Tutorial

You can store result data by YARR immediately following the tutorial.

## Basic Tutorial

- [Scan and Upload data into Local DB](tutorial-upload.md/#test)
- [Retrieve data from Local DB](tutorial-retrieve.md)

## Advanced Tutorial

- Register component data into Local DB
- Retrieve component data from ITkPD into Local DB (ITkPD Interface)
- Scan and Upload data associated with the component data into Local DB
- Register DCS data associated with the test data
- Check data in Local DB on browser (Viewer Application)
- Share data with the other Local DB (Synchronization Tool)
- Back-up Local DB (Archive Tool)

### Register Component

You can register the component data and upload test data associated with the registered component data.<br>
First please prepare connectivity file following [this sample format](config.md) and register by `dbAccessor -C -c <component connectivity file> -u <user config file> -i <site config file>`:<br>

```bash
$ cd YARR
$ ./bin/dbAccessor -C -c component.json -u user.json -i site.json
<some texts>
Do you continue to upload data into Local DB? [y/n]
y

#DB INFO# Completed the upload successfuly.
#DB INFO# -----------------------
```
> [Advanced tutorial for Component Registration](upload.md)

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
> [Advanced tutorial for retrieving funtion](retrieve.md)

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

