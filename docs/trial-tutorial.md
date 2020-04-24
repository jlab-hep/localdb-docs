# Trial Tutorial

You can try to use Local DB and Viewer Application using minimum environments and data-set on your own PC following the tutorial.

1. [Setup minimum environments and data-set on your own PC](#1-setup)
2. [Check data in Viewer Application](#2-viewer)
3. [Upload result data into Local DB](#3-upload)
4. [Retrieve data from Local DB](#4-retrieve)
5. [Download component data from ITk Production DB](#5-download-data-from-itkpd)
6. [Scan with downloaded component data](#6-scan)
7. [Upload result data of registered component data into Local DB](#7-upload-data-of-registered-component)


## 1. Setup

#### i. Clone git repository for Local DB Tools

```bash
$ git clone https://gitlab.cern.ch/YARR/YARR.git # YARR SW
$ git clone https://gitlab.cern.ch/YARR/localdb-tools.git # Local DB Tools
$ cd localdb-tools && git checkout devel
```
> Local DB Tools will be released in master branch as new version soon.

#### ii. Install requirements

You can install all requirements by running installers (need sudo).

- centOS7: [localdb-tools/setting/db_server_install.sh](https://gitlab.cern.ch/YARR/localdb-tools/-/blob/devel/setting/db_server_install.sh)
- macOS: [localdb-tools/setting/macos/installer_macos.sh](https://gitlab.cern.ch/YARR/localdb-tools/-/blob/devel/setting/macos/installer_macos.sh)

Or you can install following minimum requirements manually.

- MongoDB ([Install Manual](https://docs.mongodb.com/manual/installation/))
- Python3 & pip modules: You can install [pipi modules](requirements-list.md) by `cd localdb-tools && python3 -m pip install -r setting/requirements-pip.txt`

You should make sure following points:

- ROOT SW is installed and path to library is added. (You can confirm it by command: `root`)
- MongoDB is running. (You can confirm it by command: `mongo`)

#### iii. Download minimum data-set for trial

You can download minimum data-set prepared for this trial into your own PC.<br>

```bash
$ git clone https://gitlab.cern.ch/akubota/localdb-dataset.git  # need your account in gitlab.cern.ch
$ cd localdb-dataset
$ ./download_minimumdb.sh
```

#### iv. Replace data in MongoDB with minimum data-set

There are basically 3 ways to replace data.

- mongorestore (recommended).

```bash
$ cd localdb-dataset
$ tar xvzf localdb-dump.tar.gz
$ mongorestore --port 27017 --db localdb localdb-dump/localdb
```

- replcae directory

```bash
$ cd localdb-dataset
$ tar xvzf localdb.tar.gz

$ for centOS7
$ mv localdb /var/lib/mongo
$ sudo systemctl restart mongod

# for macOS
$ mv localdb /usr/local/var/mongodb
$ brew services restart mongodb-community@4.2
```

- build another database (advanced)

```bash
$ cd localdb-dataset
$ tar xvzf localdb.tar.gz
$ mongod --config mongod.conf &    # DB port is set to 30000
```

You can confirm if the data is replicated as follows:

```bash
$ mongo --port <Local DB port> # Local DB port is 27017 in default, but 30000 if replaced by the last way
MongoDB server version: 4.2.5
> show dbs
admin         0.000GB
config        0.000GB
local         0.000GB
localdb       0.134GB # This is Local DB replaced with minimum data-set
```

## 2. Viewer

You can check data stored in minimum data-set on browser using Viewer Application (default: http://127.0.0.1:5000/localdb/)<br>
You can setup, start, and use Viewer Application following this page: [About Viewer Application](https://localdb-docs.readthedocs.io/en/devel/viewer/)

## 3. Upload

You can upload read-out test result into Local DB after scanConsole automatically, or from specific result directory.<br>
You can just upload data from result directory prepared for this trial as follows.

```bash
$ cd localdb-dataset
$ tar xvzf fei4b-result.tar.gz
$ tar xvzf rd53a-result.tar.gz
$ cd -
$
$ cd YARR/localdb
$ ./setup_db.sh -p 27017 # specify port to Local DB
$ ./bin/localdbtool-upload scan ../../localdb-dataset/fei4b-result
$ ./bin/localdbtool-upload scan ../../localdb-dataset/rd53a-result
```
> [About setup_db.sh](setup-db.md)

You can use more features of Upload Tool (e.g. uploading results with scanConsole) following this page: [About Upload Tool](https://localdb-docs.readthedocs.io/en/devel/upload/)<br>

## 4. Retrieve

You can retrieve data from Local DB.<br>
You can setup and use Retrieve Tool following this page: [About Retrieve Tool](https://localdb-docs.readthedocs.io/en/devel/retrieve/)<br>

## 5. Download data from ITkPD

You can download component list from ITk PD into Local DB.<br>
You need ITk PD account (c.f. [Tutorial for GUI (by Andreas Heggelund)](https://indico.cern.ch/event/905734/contributions/3824355/attachments/2021113/3379403/ITKDB_GUI_Tutorial.pdf)) and administrator account for Viewer Application (c.f. [create_admin.sh](create_admin.md)).<br>

i. Go to downloading page: [http://127.0.0.1:5000/localdb/download_component](http://127.0.0.1:5000/localdb/download_component)

ii. Enter username & password for Viewer Application to enter the page.

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

You can run scanConsole with the connectivity using emulator and register the results into Local DB after scan immediately by:

```bash
$ cd YARR
$ ./bin/scanConsole -c ./db-data/connectivity.json -r ./configs/controller/emuCfg_rd53a.json -s ./configs/scans/rd53a/std_digitalscan.json -W
```

> [About scanConsole](https://localdb-docs.readthedocs.io/en/devel/scanconsole/)

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
