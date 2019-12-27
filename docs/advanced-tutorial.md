# Advanced Tutorial

- a. [Register component data into Local DB](#a-register-component)
- b. [Register component data into Local DB from ITk PD (ITkPD Interface)](#b-register-component-from-itkpd)
- c. [Scan and Upload data associated with the component data into Local DB](#c-upload-test-data)
- d. [Register DCS data associated with the test data](#d-register-dcs)
- e. [Check data in Local DB on browser (Viewer Application)](#e-check-data-on-browser)
- f. [Share data with the other Local DB (Synchronization Tool)](#f-share-data)
- g. [Back-up Local DB (Archive Tool)](#g-backup)

### a. Register Component

You can register the component data and upload the test data associated with the registered component data.<br>
First please the prepare component config file following [this sample format](config.md). <br>
And register by `dbAccessor -C -c <component connectivity file> -u <user config file> -i <site config file>`:

```bash
$ cd YARR
$ ./bin/dbAccessor -C -c component.json -u user.json -i site.json
<some texts>
Do you continue to upload data into Local DB? [y/n]
y
#DB INFO# Completed the upload successfuly.
#DB INFO# -----------------------
```
> [More detail about Upload Tool](upload.md)

### b. Register Component from ITkPD

You can download component information from ITk production database and register the info to Local DB.<br>

```bash
# 1. Set
$ cd localdb-tools
$ cd itkpd-interface
$ ./setup_interface_tool.sh

# 2. Login ITk production database
$ source authenticate.sh
Input Access Code 1 for ITkPD:
Input Access Code 2 for ITkPD:
[2019-12-27 16:05:33,138][WARNING           ]  Saved user session is expired in .auth. Creating a new one. (core.py:55)
You have signed in as <username>. Your token expires in 7197s.

# 3. Download compontnent info
$ ./bin/downloader.py --config my_conf.yml --option Module
2019-12-27 16:08:51 <hostname> <username>[2856] INFO [LDB] Found <# of component> module(s)! Start downloading...
...
2019-12-27 16:08:51 <hostname> <username>[2856] INFO [LDB] Finished!!
```



### c. scanConsole and Upload Test Data

After [the component registration](#a-register-component) (or [the registeration from ITkPD](#b-register-component-from-itkpd)),<br>
you can create the connectivity config file and the chip config files by `localdb-retrieve pull --chip <SERIAL NUMBER>`.<br>
If you have already uploaded the component test data, the config files in the latest scan are retrieved.

**This function is not available in YARR v1.1.0.**<br>
**Please change to the devel branch if want to use.**<br>

```bash
$ cd YARR
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
> [More detail about Retrieve Tool](retrieve.md)

And you can upload test data associated with the registered component data by `scanConsole` with providing the retrieved config files:

```bash
$ cd YARR
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
> [More detail about scanConsole -W](scanconsole.md)

### d. Register DCS

<!--You can register DCS data associated with the test data for each chip data.<br>
First please prepare DCS data (dcs.dat) and DCS config file (dcs_info.json) following [this sample format](config.md). <br>
And register by `dbAccessor -E`:

**This function is not available in YARR v1.1.0.**<br>
**Please change to the devel branch if want to use.**<br>

```bash
$ cd YARR
$ ./bin/dbAccessor \
-E dcs_info.json \
-s data/last_scan/scanLog.json
```
> [More detail about dbAccessor](accessor.md) -->
in edit.

### e. Check Data on Browser

You can check data in Local DB on browser using web-interface.<br>
First please run Viewer Application:

```bash
# 1. Set Application
$ cd localdb-tools
cd viewer
$ ./setup_viewer.sh

# 2. Run Application
$ ./app.py --config conf.yml &
```
> [More detail about Viewer Application](viewer.md)

And access 'http://127.0.0.1:5000/localdb/' on the local browser to check data in Local DB.

### f. Share Data

You can share data with other Local DB using Synchronization Tool.<br>
Please check [the detail page](sync.md) to get how to use.

### g. Backup

You can keep the back-up of Local DB using Archive Tool. <br>
Please check [the detail page](archive.md) to get how to use.

