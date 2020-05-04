# Trial Tutorial

You can try to use Local DB and Viewer Application using minimum environments and data-set on your own PC following the tutorial.

1. [Setup minimum environments and data-set on your own PC](#1-setup)
2. [Check data in Viewer Application](#2-viewer)
3. [Upload result data into Local DB](#3-upload)
4. [Retrieve data from Local DB](#4-retrieve)
5. [Download component data from ITk Production DB](#5-download-data-from-itkpd)
6. [Scan with downloaded component data](#6-scan)
7. [Upload result data of registered component data into Local DB](#7-upload-data-of-registered-component)

## 0. Requirements

- Python3 & pip modules: You can install [pipi modules](requirements-list.md) by `cd localdb-tools && python3 -m pip install -r setting/requirements-pip.txt`

## 1. Setup

#### i. Clone git repository for this tutorial

You can download MongoDB Packages and minimum data-set for Local DB by following script.

- `setup_all.sh`: download MongoDB Packages and minimum data-set
  - `install_mongo.sh`: download MongoDB Packages
  - `download_minimumdb.sh`: download minimum data-set

```bash
$ git clone https://gitlab.cern.ch/akubota/localdb-dataset.git  # need your account in gitlab.cern.ch
$ cd localdb-dataset
$ ./seup_all.sh
[LDB] Select your OS from the list. (Type a-d from the list)

OS supported by tutorial
  a) RHEL 6.2 Linux x64
  b) RHEL 7.0 Linux x64
  c) macOS x64
OS not supported by tutorial
  d) Others

[LDB] > a    ### Set a if you are trying on lxplus server
<some texts>
[LDB] Done.
[LDB] Check README to get how to use commands in ./mongodb-4.2.6/bin

[LDB] To make a path to commands in ./mongodb-4.2.6/bin you have to excute:
[LDB] export PATH=path/to/mongodb-4.2.6/bin:$PATH"

$ export PATH=path/to/mongodb-4.2.6/bin:$PATH
```

#### ii. Start MongoDB Server

```bash
$ pwd
path/to/localdb-dataset

# To start the MongoDB server if you do the tutorial on lxplus you have to run
$ ./mongodb-4.2.6/bin/mongod --config mongod.conf &
$ cat mongod.conf | grep port
27017 # This number is port to MongoDB server

# Confirmation of running MongoDB server
$ ./mongodb-4.2.6/bin/mongo --port 27017 # Specify port number to MongoDB server
MongoDB shell version v4.2.6
> show dbs
admin    0.000GB
config   0.000GB
local    0.000GB
localdb  0.134GB # Succeeded if you can check this repository
```

## 2. Viewer

You can check data stored in minimum data-set on browser using Viewer Application.<br>

#### i. Setup

```bash
$ git clone https://gitlab.cern.ch/YARR/localdb-tools.git # Local DB Tools
$ cd localdb-tools && git checkout devel
```

#### ii. Create admin account for Local DB

```bash
$ pwd
path/to/localdb-tools
$ cd setting
$ ./create_admin.sh -p <port to MongoDB server>
# e.g. ./create_admin.sh -p 27017
Authentication succeeded!
Local DB Server IP address: 127.0.0.1
Local DB Server port: 27017

Are you sure thats correct? [y/n] ### Enter y
> y

Register localDB admins username: USERNAME  ### Input your favorite username
Register localDB admins password:           ### Input your favorite password
Successfully added user:
<some texts>

$ cd -
```

#### iii. Create config file for Viewer Application

```bash
$ pwd
path/to/localdb-tools
$ cd viewer
$ ./setup_viewer.sh -p 27017
Local DB Server IP address: 127.0.0.1
Local DB Server port: 27017

[LDB] Are you sure thats correct? [y/n] ### Enter y
> y

[LDB] Welcome to Local Database Tools!
...
[LDB] Do you use admin functions for LocalDB viewer? [y/n] ### Enter y
> y

Input localDB admins username: USERNAME ### Input admin username set in create_admin.sh
Input localDB admins password:          ### Input admin password set in create_admin.sh

<some texts>

$[LDB] Start Viewer Application by ...
$[LDB]   python3 app.py --config admin_conf.yml
```

#### iv. Start Viewer Application

```bash
$ pwd
path/to/localdb-tools/viewer
$ python3 app.py --config admin_conf.yml
Need user authentication.
Authentication succeeded.
2020-01-31 23:25:23 localdbserver.cern.ch matplotlib.font_manager[18847] INFO generated new fontManager
2020-01-31 23:25:23 localdbserver.cern.ch root[18847] INFO [LDB] Viewer Application URL: http://127.0.0.1:5000/localdb/
 * Serving Flask app "app" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
2020-01-31 23:25:24 localdbserver.cern.ch werkzeug[18847] INFO  * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

And you can check Viewer on browser: http://127.0.0.1:5000/localdb/

#### v. SSH Tunnel (for trying on lxplus server)

```bash
# on lxplus server
$ ip address
# -> get IP address to lxplus server (eth0.inet)
```

```bash
# on your local PC
$ ssh -L <unused port number>:localhost:<port number to Viewer Application on lxplus> <username>@<ipaddress to lxplus server> -fN
# e.g. ssh -L 5000:localhost:5000 user@127.0.0.1 -fN
```

Then you can check viewer on browser on your local PC: http://127.0.0.1:5000/localdb/

#### vi. Additional information

[About Viewer Application](https://localdb-docs.readthedocs.io/en/devel/viewer/)

## 3. Upload

You can upload read-out test result into Local DB after scanConsole automatically, or from specific result directory.<br>

#### i. Setup

```bash
$ git clone https://gitlab.cern.ch/YARR/YARR.git
$ cd YARR

### step1. compile YARR commands
$ mkdir build && cd build
$ cmake3 ../
$ make -j4
$ make install
$ cd ../
# If you could not proceed according to your environmental problems,
# you can skip here and go to step2.

### step2.
$ cd localdb
$ ./setup_db.sh -p 27017 # specify port to MongoDB server
$ cd ../
```
> [About setup_db.sh](setup-db.md)

#### ii. Confirmation

```bash
$ pwd
path/to/YARR

$ ./localdb/bin/localdbtool-upload init
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017/localdb
#DB INFO# ---> Connection is GOOD.
#DB INFO# -----------------------

### If you could compile YARR commands
$ ./bin/dbAccessor -I
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017/localdb
#DB INFO# ---> Connection is GOOD.
#DB INFO# -----------------------
```

#### iii. Upload

##### iii-a. Upload w/ scanConsole (If you could compile YARR commands)

You can upload results into Local DB after scanConsole just by adding option '-W'.

```bash
$pwd
path/to/YARR

### FEI4B emulator
$ ./bin/scanConsole \
-c configs/connectivity/example_fei4b_setup.json \
-r configs/controller/emuCfg.json \
-s configs/scans/fei4/std_digitalscan.json \
-W

### RD53A emulator
$ ./bin/scanConsole \
-c configs/connectivity/example_rd53a_setup.json \
-r configs/controller/emuCfg_rd53a.json \
-s configs/scans/rd53a/std_digitalscan.json \
-W
```

Check if your result is uploaded in Viewer Application: http://127.0.0.1:5000/localdb/scan

##### iii-b. Upload w/o scanConsole (If you could not compile YARR commands)

You can just upload data from result directory prepared for this trial as follows even if you could not compile YARR commands.

```bash
$ cd localdb-dataset
$ tar xvzf fei4b-result.tar.gz
$ tar xvzf rd53a-result.tar.gz

$ cd YARR
$ ./localdb/bin/localdbtool-upload scan path/to/localdb-dataset/fei4b-result
$ ./localdb/bin/localdbtool-upload scan path/to/localdb-dataset/rd53a-result
```

#### iv. Additional information

[About Upload Tool](https://localdb-docs.readthedocs.io/en/devel/upload/)<br>

## 4. Retrieve

You can retrieve data from Local DB.<br>

#### i. Retrieve test log

```bash
$ pwd
path/to/YARR
$ ./localdb/bin/localdbtool-retrieve log
```

#### ii. Retrieve data files

```bash
$ pwd
path/to/YARR
$ ./localdb/bin/localdbtool-retrieve pull
```

#### iii. Retrieve/Create config files for registered component

You can register component data by downloading from ITkPD. (See [5. Download data from ITkPD](#5-download-data-from-itkpd)

```bash
$ pwd
path/to/YARR
$ ./localdb/bin/localdbtool-retrieve pull --chip <serial number>
# e.g. ./localdb/bin/localdbtool-retrieve pull --chip RD53A-001
```

#### iv. Additional information

[About Retrieve Tool](https://localdb-docs.readthedocs.io/en/devel/retrieve/)<br>

## 5. Download data from ITkPD

You can download component list from ITk PD into Local DB.<br>
You need ITk PD account (c.f. [Tutorial for GUI (by Andreas Heggelund)](https://indico.cern.ch/event/905734/contributions/3824355/attachments/2021113/3379403/ITKDB_GUI_Tutorial.pdf)) and administrator account for Viewer Application (c.f. [create_admin.sh](create_admin.md)).<br>

i. Go to downloading page: [http://127.0.0.1:5000/localdb/download_component](http://127.0.0.1:5000/localdb/download_component)

ii. Enter admin username & password for Viewer Application to enter the page. (admin is registered [here](#ii-create-admin-account-for-local-db))

iii. Enter 2 Access codes for ITk PD.

iv. Push button 'Download component info'

v. Finish and you can check component lists in the component page on browser.

You can check more detail here: [Demonstration Docs](https://qc-demonstration.readthedocs.io/en/latest/database_demonstration_download_itkpd/).

## 6. Scan

You can retrieve component data from Local DB, scan it, and store the results associated with the module data into Local DB.<br>

#### i. Setup database config

If you already setup db config in [Step 3. Upload](#3-upload), you can skip here.

```bash
$ cd YARR/localdb
$ ./setup_db.sh -p 27017 # specify port to Local DB
```
> [About setup_db.sh](setup-db.md)

#### ii. Generate connectivity config file

You can generate connectivity config file for the module data registered in Local DB.<br>
Here, let's try it for RD53A Quad Module (ATLAS SN: 20UPGRQ0000129)

```bash
$ cd YARR
$ ./localdb/bin/localdbtool-retrieve pull --chip 20UPGRQ0000129
# -> generate config file in ./db-data.
```

> [About Retrieve Tool](https://localdb-docs.readthedocs.io/en/devel/retrieve/)

#### iii. Modify connectivity config file

You have to change stage name in connectivity config file as follows:

```json
{
    "stage": "ENCAPSULATION",
    "chips": [
        {
            "config": "./db-data/20UPGRA0000723.json",
            "tx": 0,
            "rx": 0
        },
        {
            "config": "./db-data/20UPGRA0000724.json",
            "tx": 0,
            "rx": 1
        },
        {
            "config": "./db-data/20UPGRA0000725.json",
            "tx": 0,
            "rx": 2
        },
        {
            "config": "./db-data/20UPGRA0000726.json",
            "tx": 0,
            "rx": 3
        }
    ],
    "module": {
        "serialNumber": "20UPGRQ0000129",
        "componentType": "module"
    },
    "chipType": "RD53A"
}
```
> stage list: "PALYLENE_COATING", "ENCAPSULATION", "THERMAL_CYCLING"

#### iv. Scan

##### iv-a. Scan w/ scanConsole (If you could compile YARR commands)

You can run scanConsole with the connectivity using emulator and register the results into Local DB after scan immediately by:

```bash
$ cd YARR
$ ./bin/scanConsole -c ./db-data/connectivity.json -r ./configs/controller/emuCfg_rd53a.json -s ./configs/scans/rd53a/std_digitalscan.json -W
```

> [About scanConsole](https://localdb-docs.readthedocs.io/en/devel/scanconsole/)

##### iv-b. Scan w/ scanConsole.sh (If you could not compile YARR commands)

If you cannot run emulator on your own PC, you can just generate scan-like results under data/last_scan using a script `scanConsole.sh`. (c.f. [localdb-dataset/scanConsole.sh](https://gitlab.cern.ch/akubota/localdb-dataset/-/blob/master/scanConsole.sh))<br>
You can run it after moving the script under YARR directory from localdb-dataset as follows:

```bash
$ mv ./localdb-dataset/scanConsole.sh ./YARR/
$ cd YARR
$ ./scanConsole.sh -c ./db-data/connectivity.json -s digitalscan -W
```
> you can specify scan type from [ "digitalscan", "analogscan", "thresholdscan", "totscan" ] under option '-s'<br>
> you can upload results after scan immediately with option '-W', or just generate scan-like results without option '-W'

You can check more detail here: [Demonstration Docs](https://qc-demonstration.readthedocs.io/en/latest/database_demonstration_setup_for_scan/).

## 7. Upload data of registered component

You can push registered results from Local DB into ITk PD in the production.<br>
PD Upload Tool is currently under development.<br>
Here, just try to select the results for uploading.<br>

i. Do all necessary scans ("std_digital_scan", "std_analog_scan", "std_threshold_scan", "std_tot_scan")

ii. Go to selection page: [http://127.0.0.1:5000/localdb/select_test](http://127.0.0.1:5000/localdb/select_test)

iii. Enter module name ("20UPGRQ0000129") and stage name ("ENCAPSULATION")

iv. Select one resule for each test item

v. Push button 'Confirm'

vi. Push button 'Register' after confirmation

You can check more detail here: [Demonstration Docs](https://qc-demonstration.readthedocs.io/en/latest/database_demonstration_upload_itkpd/).
