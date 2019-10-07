# Local DB Tools Installation

There are several tools for handling Local DB.

* Uploader ---> [YARR](#yarr)<br>
    To upload data (test data, chip data, user data, site data ...) into Local DB.

* Retriever ---> [YARR](#yarr)<br>
    To retrieve data (data log, data files) from Local DB.

* Viewer Application ---> [Local DB Tools](#local-db-tools)<br>
    To check/edit data in Local DB on browser.

* Synchronization Tool ---> [Local DB Tools](#local-db-tools)<br>
    To push/pull/share data with the other Local DB or Master Server (Centralize Local DB).

* Archive Tool ---> [Local DB Tools](#local-db-tools)<br>
    To create archive tar.gz file for Local DB back-up.

## YARR

There are two Local DB tools included in YARR SW.

* Uploader
* Retriever 

### 0. YARR SW Installation

Please check [YARR SW Installation](https://yarr.readthedocs.io/en/latest/install/) to install and set-up. <br>

### 1. Set-up Local DB

`YARR/localdb/setup_db.sh` can set-up Local DB setting in user local environments by following steps:

* Create the user directory for Local DB ---> ${HOME}/.yarr/localdb
* Create the database config file ---> [${HOME}/.yarr/localdb/${HOSTNAME}_database.json](config.md)
* Check if required python modules are installed

```bash
$ cd YARR
$ ./localdb/setup_db.sh
[LDB] Confirmation
<some texts>
[LDB] Continue? [y/n]
[LDB] > y
<some texts>
[LDB] Create Config file...
[LDB] DB Config: ${HOME}/.yarr/localdb/${HOSTNAME}_database.json
[LDB] Done.
<some texts>
[LDB] More detail:
[LDB]   Access 'https://localdb-docs.readthedocs.io/en/master/'
```

<details><summary> Additional options </summary>

- **-i ``<IP address>``** : Set Local DB server IP address (default: 127.0.0.1) 
- **-p ``<port>``** : Set Local DB server port (default: 27017)
- **-n ``<DB name>``** : Set Local DB Name (default: localdb)
- **-a ``<CA file>``** : Path to CA certificate of Local DB server (option)
- **-e ``<Certification>``** : Path to Client certificate of Local DB server (option)
- **-r** : Clean the settings (reset)

</details>

### 2. Confirmation

Please run the command with the option 'init' to check if the command is working or the connection to Local DB is good.

```bash
$./localdb/bin/localdbtool-upload init
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# Local DB Server: mongodb://127.0.0.1:27017/localdb
#DB INFO# ---> connection is good.
#DB INFO# -----------------------
$
$./localdb/bin/localdbtool-retrieve init
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017
#DB INFO#    The connection is GOOD.
#DB INFO# -----------------------
```

If an error occurs, please check [FAQ]().

## Local DB Tools

There are three Local DB tools included in YARR SW.

* Viewer Application
* Synchronization Tool
* Archive Tool

### 0. SW Installation

```bash
$ git clone https://gitlab.cern.ch/YARR/localdb-tools.git
```

### 1.1 Set-up Viewer Application

`localdb-tools/viewer/setup_viewer.sh` can set-up Viewer Application setting in user local environments by following steps:

* Create the viewer config file ---> [localdb-tools/viewer/conf.yml](config.md)
* Check if required python modules are installed

```bash
$ cd localdb-tools/viewer
$ ./setup_viewer.sh
<some texts>
[LDB] Are you sure that is correct? [y/n]
> y
<some texts>
[LDB] More information: https://localdb-docs.readthedocs.io/en/master/
```

<details><summary> Additional options </summary>

- **-i ``<IP address>``** : Set Local DB server IP address (default: 127.0.0.1) 
- **-p ``<port>``** : Set Local DB server port (default: 27017)
- **-c ``<cfg>``** : Set config file Name (default: conf.yml)

</details>

### 1.2 Set-up Synchronization Tool

### 1.3 Set-up Archive Tool

