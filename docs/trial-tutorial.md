# Trial Tutorial

You can try to use Local DB and Viewer Application using minimum environments and data-set on your own PC following the tutorial.

1. [Setup minimum environments and data-set on your own PC](#1-setup)
2. [Check data in Viewer Application](#2-viewer)
3. [Upload result data into Local DB](#3-upload)
4. [Retrieve data from Local DB](#4-retrieve)
5. [Register component data into ITk Production DB](#5-register-into-itkpd)
6. [Retrieve component data from ITk Production DB](#6-retrieve-from-itkpd)
7. [Upload result data of registered component data into Local DB](#7-upload-data-of-registered-component)


### 1. Setup

#### i. Clone git repository for Local DB Tools

```bash
$ git clone https://gitlab.cern.ch/YARR/YARR.git # YARR SW
$ git clone https://gitlab.cern.ch/YARR/localdb-tools.git # Local DB Tools
$ cd localdb-tools && git checkout devel
```

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

### 2. Viewer

You can check data stored in minimum data-set on browser using Viewer Application.<br>
You can setup, start, and use Viewer Application following this page: [About Viewer Application](https://localdb-docs.readthedocs.io/en/devel/viewer/)

### 3. Upload

You can upload read-out test result into Local DB after scanConsole automatically, or from specific result directory.<br>
You can setup and use Upload Tool following this page: [About Upload Tool](https://localdb-docs.readthedocs.io/en/devel/upload/)<br>
Or you can just upload data from result directory prepared for this trial as follows.

```bash
$ cd localdb-dataset
$ tar xvzf result-fei4b.tar.gz
$ tar xvzf result-rd53a.tar.gz
$ cd -
$
$ cd YARR/localdb
$ ./setup_db.sh -p 27017 # specify port to Local DB
$ ./bin/localdbtool-upload scan ../../localdb-dataset/result-fei4b
$ ./bin/localdbtool-upload scan ../../localdb-dataset/result-rd53a
```

### 4. Retrieve

You can retrieve data from Local DB.<br>
You can setup and use Retrieve Tool following this page: [About Retrieve Tool](https://localdb-docs.readthedocs.io/en/devel/retrieve/)<br>

### 5. Register into ITkPD

in edit.

### 6. Retrieve from ITkPD

in edit.

### 7. Upload data of registered component

in edit.

