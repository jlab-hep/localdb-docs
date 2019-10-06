## About

**Local Database (Local DB) is mainly data managing system for YARR based on MongoDB.**

### Base system
- [MongoDB](https://docs.mongodb.com/v4.0/) v4.0.11
- Python3 
- PyROOT (executable by Python3)

The setting scripts and instructions supports the following OS:

- centOS7

## Quick Tutorial

You can store result data by YARR immediately following the tutorial.

### 0. Installation

This step should be done by the administrator of the machine.<br>
The detail can be checked [Quick Installtion](#quick-installation).

### 1. Setup YARR command with Local DB

```bash
$ cd YARR
$ git checkout devel
$ mkdir build
$ cd build
$ cmake3 ../
$ make -j4
$ make install
$ cd ../
```

### 2. Setup Local DB Directory

- Set Local DB directory by `setup_db.sh`.

```bash
$ ./localdb/setup_db.sh
[LDB] Confirmation
<some texts>
[LDB] Continue? [y/n]
[LDB] > y
<some text>
[LDB] This description is saved as ${HOME}/YARR/localdb/README
```

- Confirme Local DB tools

```bash
$ ./localdb/bin/localdbtool-upload init
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# Local DB Server: mongodb://127.0.0.1:27017
#DB INFO# ---> connection is good.
#DB INFO# -----------------------
```

If there are some problems in the step, [FAQ](#faq) should be helpful for solving it.

### 3. scanConsole with Local DB

- scanConsole
   
You can scan and upload result data into Local DB by `scanConsole -W`

```bash
$ ./bin/scanConsole \
-r configs/controller/emuCfg.json \
-c configs/connectivity/example_fei4b_setup.json \
-s configs/scans/fei4/std_digitalscan.json \
-W
<lots of text>
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# Local DB Server: mongodb://127.0.0.1:27017
#DB INFO# ---> connection is good.
#DB INFO# -----------------------
#DB INFO# Uploading in the back ground. (log: ~/.yarr/localdb/log/)
```

Additional options:

- **-d ``<database config>``** : Set database config file (default: `${HOME}/.yarr/localdb/${HOSTNAME}_database.json`)
- **-u ``<user config>``** : Set user config file ([sample](#user-config-file))
- **-i ``<site config>``** : Set site config file ([sample](#site-config-file))

- Confirmation

There are three ways to confirm the data uploaded.

1. Log File
   
You can check if the upload is success in log file `${HOME}/.yarr/localdb/log/day.log`.

```log
2019-08-01 10:55:46,821 - INFO: -----------------------
2019-08-01 10:55:46,821 - INFO: Function: Upload Scan Data
2019-08-01 10:55:46,823 - INFO: Local DB Server: mongodb://127.0.0.1:27017
2019-08-01 10:55:46,826 - INFO: ---> connection is good.
2019-08-01 10:55:46,826 - INFO: Cache Directory: /home/akubata/work/YARR/data/000186_std_digitalscan/
2019-08-01 10:55:47,058 - INFO: Success
2019-08-01 10:55:47,060 - INFO: -----------------------
```

2. Retrieve Tool

You can check uploaded test log in CUI command `localdb/bin/localdbtool-retrieve`.

```bash
$ ./localdb/bin/localdbtool-retrieve log 
#DB INFO# -----------------------
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017
#DB INFO#    The connection is GOOD.
test data ID: 5d4c94c1fd212a639247b044 
User      : arisa_kubota at tokyo_institute_of_technology
Date      : 2019/08/08 14:31:39
Chip      : RD53A-001, RD53A-001_chip1
Run Number: 255
Test Type : std_analogscan
DCS Data  : NULL

test data ID: 5d4c89a4e34d9efb40565e65 
User      : arisa_kubota at tokyo_institute_of_technology
Date      : 2019/08/08 13:44:14
Chip      : RD53A-001, RD53A-001_chip1
Run Number: 251
# Ctrl+C can terminate the output test log
```

3. Viewer Application

You can check uploaded test data in GUI when Viewer Application is running. ([How to run the Viewer Application](#viewer-application))<br>
Access `http://127.0.0.1:5000/localdb/` or `http://IPaddress/localdb` in browser.

## Advanced Tutorial

### Chip Registration

You can store results associated with the registered chip after the registration. <br>
Prepare the component information file and user information file.<br>

- user config file (json) ([sample](#user-config-file))
- site config file (json) ([sample](#site-config-file))
- component config file (json) ([sample](#component-config-file))

And run the `dbAccessor -C`:

```bash
$ ./bin/dbAccessor -C -c component.json -u user.json -i site.json
<some texts>
Do you continue to upload data into Local DB? [y/n]
y

#DB INFO# Completed the upload successfuly.
#DB INFO# -----------------------
```

Additional options:

- **-d ``<database config>``** : Set database config file (default: `${HOME}/.yarr/localdb/${HOSTNAME}_database.json`)
- **-u ``<user config>``** : Set user config file ([sample](#user-config-file))
- **-i ``<site config>``** : Set site config file ([sample](#site-config-file))

This can register the components data written in component.json.

### Module Registration

You can store results associated with the registered module after the registration. <br>
Prepare the component information file and user information file.<br>

- user config file (json) ([sample](#user-config-file))
- site config file (json) ([sample](#site-config-file))
- component config file (json) ([sample](#component-config-file))

And run the `dbAccessor -C`:

```bash
$ ./bin/dbAccessor -C -c component.json -u user.json -i site.json
<some texts>
Do you continue to upload data into Local DB? [y/n]
y

#DB INFO# Completed the upload successfuly.
#DB INFO# -----------------------
```

Additional options:

- **-d ``<database config>``** : Set database config file (default: `${HOME}/.yarr/localdb/${HOSTNAME}_database.json`)
- **-u ``<user config>``** : Set user config file ([sample](#user-config-file))
- **-i ``<site config>``** : Set site config file ([sample](#site-config-file))

This can register the components data written in component.json.

### scanConsole with registered Module

Connecivity config and chip config file should be prepared properly.

- connectivity config (json) ([sample](#connectivity-config-file))
- chip config (json) ([sample](#chip-config-file))

And run the `scanConsole`:

```bash
$ ./bin/scanConsole \
-r configs/controller/emuCfg.json \
-c configs/connectivity.json \
-s configs/scans/fei4/std_digitalscan.json \
-W \
-i site.json \
-u user.json
<Lots of text>
```

After that, you can check the result (registered component) in Module/Test Page of Viewer Application.

### DCS Registration

You can store DCS data associated with the scan data for each chip data. <br> 
Prepare the DCS config file, DCS data file, scan log file.<br>

- DCS config (json) ([sample](#dcs-config-file))
- DCS data (dat or csv) ([sample](#dcs-data-file))
- scan log (json) ([sample](#scan-log-file))

In general, scan log should be `scanLog.json` of the specific test generated by scanConsole.

And run the `dbAccessor -E`:

```bash
$ ./bin/dbAccessor \
-E dcs_info.json \
-s data/last_scan/scanLog.json \
DBHandler: Register Environment:
	environmental config file : dcs_info.json
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# Local DB Server: mongodb://127.0.0.1:27017
#DB INFO# ---> connection is good.
#DB INFO# -----------------------
#DB INFO# Uploading in the back ground. (log: ~/.yarr/localdb/log/)
```

Additional options:

- **-d ``<database config>``** : Set database config file (default: `${HOME}/.yarr/localdb/${HOSTNAME}_database.json`)
- **-u ``<user config>``** : Set user config file ([sample](#user-config-file))
- **-i ``<site config>``** : Set site config file ([sample](#site-config-file))

## Local DB Tools
|Function      |Tool Name           |Command             |
|:------------:|:------------------:|:------------------:|
|Storage System|Local DB            |mongo               |
|Store Data    |Upload Tool         |localdbtool-upload  |
|Restore Data  |Retrieve Tool       |localdbtool-retrieve|
|Share Data    |Synchronization Tool|localdbtool-sync    |
|Check Data    |Viewer Application  |python app.py       |

### Retrieve Tool

#### Check Connection

```bash
$ ./localdb/bin/localdbtool-retrieve init
```

Additional options:

- **--database ``<database config>``** : Set database config file (default: `${HOME}/.yarr/localdb/${HOSTNAME}_database.json`)

#### Check Test Log

```bash
$ ./localdb/bin/localdbtool-retrieve log
```

Additional options:

- **--database ``<database config>``** : Set database config file (default: `${HOME}/.yarr/localdb/${HOSTNAME}_database.json`)
- **--user ``<user config>``** : Set user config file
- **--site ``<site config>``** : Set site config file
- **--chip ``<chip name>``** : Set chip name

#### Retrieve Config File

in edit

### Upload Tool

#### Check Connection

```bash
$ ./localdb/bin/localdbtool-upload init
```

Additional options:

- **--database ``<database config>``** : Set database config file (default: `${HOME}/.yarr/localdb/${HOSTNAME}_database.json`)
 
#### Upload Scan 

You can upload data from the result directory of YARR by `localdbtool-upload`.

**This function supports not only uploading from the result directory generated by `scanConsole -W` but also uploading from the result directory generated by `scanConsole`.** <br>
**But in uploading from the result directory generated by `scanConsole`, there might be some loss in the uploaded data.**

```bash
$ ./localdb/bin/localdbtool-upload scan <path/to/result/dir>
e.g.) $ ./localdb/bin/localdbtool-upload scan ./data/last_scan
```

Additional options:

- **--database ``<database config>``** : Set database config file (default: `${HOME}/.yarr/localdb/${HOSTNAME}_database.json`)
- **--user ``<user config>``** : Set user config file
- **--site ``<site config>``** : Set site config file
- **--log** : Set logging mode (default 'False'). If set 'True', the output log is written in `${HOME}/.yarr/localdb/log/day.log`
- **--username ``<username>``** : Set username of the Local DB Server if the users authenticated is needed
- **--password ``<password>``** : Set password of the Local DB Server if the users authenticated is needed
- **--config ``<config file>``** : Set config file which username and password are written in if the users authenticated is needed

#### Upload Cache

When you could not upload Scan/DCS data by `scanConsole -W`/`dbAccessor -E` because of the bad connection to Local DB Server,<br>
the cache data and log file ('scanLog.json'/'dbDcsLog.json') would be stored in the result directory,<br> 
and that record is written to the file: `${HOME}/.yarr/run.dat`/`${HOME}/.yarr/dcs.dat`. 

In the good connection to Local DB Server, you can upload all cache data by `localdbtool-upload cache`

```bash
$ ./localdb/bin/localdbtool-upload cache
```
   
#### Check Registered Component Data

You can check all component data registered in Local DB Server by `localdbtool-upload check`

```bash
$ ./localdb/bin/localdbtool-upload check comp
```

#### Check Chip Data

You can check all chip data tested by `localdbtool-upload check`

```bash
$ ./localdb/bin/localdbtool-upload check chip
```

## Quick Installation 

### Installation for Local DB Server

Reference: [Install MongoDB](https://docs.mongodb.com/manual/installation/)<br>
Local DB Supports mongo DB server Ver. 4.X or more.

- For centOS7

1. Add yum repository `/etc/yum.repos.d/mongodb-org-4.2.repo`

```bash
[mongodb-org-4.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.2/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-4.2.asc
```

2. Install by yum

```bash
$ sudo yum install -y mongodb-org.x86_64
```

3. Directories (default)

- shell command: `/bin/mongo`
- process command: `/bin/mongod`
- config file: `/etc/mongod.conf`
- data directory: `/var/lib/mongo`
- log directory: `/var/log/mongodb`

4. Start MongoDB

```bash
$ sudo service mongod start
```

5. Verify that MongoDB has started successfully

```bash
$ mongo
MongoDB shell version v4.0.11
<some texts>
> 
```

If you want to enable access authorization, check [Access Authorization](#access-authorization)

- For MacOS

1. Install Homebrew

2. Tap the MongoDB Homebrew Tap

```bash
$ brew tap mongodb/brew
```

3. Install MongoDB

```bash
$ brew install mongodb-community@4.0
```

4. Directories (default)

- shell command: `/usr/local/opt/mongodb-community\@4.0/bin/mongo`
- process command: `/usr/local/opt/mongodb-community\@4.0/bin/mongod`
- config file: `/usr/local/etc/mongod.conf`
- data directory: `/usr/local/var/lib/mongo`
- log directory: `/usr/local/var/log/mongodb`

5. Start MongoDB

```bash
$ brew services start mongodb-community@4.0
```

6. Verify that MongoDB has started successfully

```bash
$ export PATH=$PATH:/usr/local/opt/mongodb-community\@4.0/bin
$ mongo
MongoDB shell version v4.0.11
<some texts>
> 
```

### Installation of Local DB Tools

[Local DB Tools repository](https://github.com/jlab-hep/localDB-tools)

```bash
$ git clone https://github.com/jlab-hep/localDB-tools.git
$ cd localDB-tools/setting
$ sudo pip3 install -r requirements-pip.txt
```

#### Viewer Application

Web Application which can check data stored in Local DB.

```bash
$ cd localDB-tools/viewer
$ ./setup_viewer.sh
$ python3 app.py --config conf.yml &
```

Check `http://localhost:5000/localdb/` in local browser.<br>
If you want to check data remotely, check [here](#remote-connection)

#### Synchronization Tool

Command which can synchroniza data between other Local DB Server.

## Remote Connection

Local DB supports two methods to connect remotely:

- SSL/TLS Connection
- SSH Tunnel

### SSL/TLS Connection (Recommended)

See [MongoDB documentation for TLS/SSL](https://docs.mongodb.com/manual/tutorial/configure-ssl/) for more information.

#### Requirements for DB Server

- Open the TCP port (e.g. 27017) used by mongod service 

```bash
$ sudo firewall-cmd --zone=public --add-port=27017/tcp --permanent
$ sudo firewall-cmd --reload
```

- Create x.509 certificate for server

See 
[Create CA PEM file](https://docs.mongodb.com/manual/appendix/security/appendixA-openssl-ca/) and 
[Create Server Certificates](https://docs.mongodb.com/manual/appendix/security/appendixB-openssl-server/#appendix-server-certificate).

```bash
$ sudo cp path/to/CA/file /etc/ssl/localdb_ca.pem
$ sudo cp path/to/certificate/file /etc/ssl/localdb_cert.pem
```

- Stop MongoDB

```bash
$ sudo systemctl stop mongod
$ sudo vim /etc/mongod.conf
```

- Set SSL mode (For MongoDB version 4.0 and earlier)

```yaml
# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1, "DB SERVER HOSTNAME"
  ssl:
    mode: requireSSL
    PEMKeyFile: /etc/ssl/localdb_cert.pem ### Server Certificate
    CAFile: /etc/ssl/localdb_ca.pem ### CA PEM File
```

- Set TLS mode (For MongoDB version 4.2 and greater)

```yaml
# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1, "DB SERVER HOSTNAME"
  tls:
    mode: requireTLS
    certificateKeyFile: /etc/ssl/localdb_cert.pem ### Server Certificate
    CAFile: /etc/ssl/localdb_ca.pem ### CA PEM File
```

- Start MongoDB

```bash
$ sudo systemctl restart mongod.service
```

- Confirmation

```bash
# For MongoDB version 4.0 and earlier
$ mongo --ssl --sslPEMKeyFile /etc/ssl/localdb_cert.pem --sslCAFile /etc/ssl/localdb_ca.pem --sslAllowInvalidHostnames --port 27017
# For MongoDB version 4.2 and greater
$ mongo --tls --tlsCertificateKeyFile /etc/ssl/localdb_cert.pem --tlsCAFile /etc/ssl/localdb_ca.pem --tlsAllowInvalidHostnames --port 27017
```

- Create x.509 certificate for client 

See [Create Client Certificates](https://docs.mongodb.com/manual/appendix/security/appendixC-openssl-client/#appendix-client-certificate).

Send the client certificate and CA file to the client machine.

#### Remote Connection from the client machine

- Receive x.509 certificate for client 

- Confirmation

```bash
# For MongoDB version 4.0 and earlier
$ mongo --ssl --sslPEMKeyFile /etc/ssl/localdb_cert.pem --sslCAFile /etc/ssl/localdb_ca.pem --sslAllowInvalidHostnames --port 27017 --host "DB SERVER HOSTNAME"
# For MongoDB version 4.2 and greater
$ mongo --tls --tlsCertificateKeyFile /etc/ssl/localdb_cert.pem --tlsCAFile /etc/ssl/localdb_ca.pem --tlsAllowInvalidHostnames --port 27017 --host "DB SERVER HOSTNAME"
```

### SSH Tunnel

#### Requirements for DB Server

- Stop MongoDB

```bash
$ sudo systemctl stop mongod
$ sudo vim /etc/mongod.conf
```

- Set SSL mode (For MongoDB version 4.0 and earlier)

```yaml
# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1, "DB SERVER HOSTNAME"
```

- Start MongoDB

```bash
$ sudo systemctl restart mongod.service
```

- Create ssh user for the client

```bash
$ sudo useradd <username>
$ sudo passwd <username>
```

#### Remote Connection from the client machine

- Connect to the DB Server by SSH Tunnel

```bash
$ ssh -L 27018:localhost:27017 "DB SERVER HOSTNAME" -fN
```

- Confirmation

```bash
$ mongo --port 27018 
```

## Access Authorization

in edit


## FAQ 

### the detail of 'setup_db.sh'

`setup_db.sh` can set Local DB commands and the default configuration files for Local DB.

```bash
$ cd YARR
$ ./localdb/setup_db.sh
[LDB] Check the exist site config...NG!

[LDB] Enter the institution name where this machine is, or 'exit' ... 
> INSTITUTION NAME
```

Additional command line arguements:
    
- **-h** : this, prints all available command line arguments
- **-i  ``<IP address>``** : Set IP address of the Local DB Server (default: 127.0.0.1)
- **-p  ``<port number>``** : Set port number of the Local DB Server (default: 27017)
- **-n  ``<database name>``** : Set the Local DB Server Name (default: 'localdb')
- **-r** : Rseet the all settings for Local DB

### '[LDB] Error checking python modules! Exit!'

You are missing some python modules incuded in the requirements.<br>
Check which python module missing by `python3 check_python_modules.py`

```bash
$ python3 check_python_modules.py 
[LDB] Welcome to Local Database Tools!
[LDB] Check Python version ... 3.6 ... OK!
[LDB] Check python modules: 
<some texts>
	requests...not found
	tzlocal...OK!
```

`<module name>...not found!` suggests that `<module name>` is missing,
so install the module by `$ sudo pip3 install <module name>` or `$ pip3 install --user <module name>`.

### '#DB ERROR# The connection of Local DB mongodb://127.0.0.1:27017 is BAD.'

Connection check by `localdbtool-upload init` is failed by some reasons.

1. Uncompleted the setup of Local DB Server

You can check is as following:

```bash
$ mongo
# i. MongoDB not installed
bash: mongo: command not found

# ii. MongoDB not started
<some texts>
exception: connect failed
```

1. MongoDB not installed

You can setup Local DB Server automatically by the script:

```bash
$ git clone https://github.com/jlab-hep/localDB-tools.git
$ cd localDB-tools/setting
$ sudo ./db_server_install.sh
```

Check [Setup Local DB Server](#setup-local-db-server) for more detail.

2. MongoDB not started

You can start/restart/enable Mongo DB by systemctl (centOS7):

```bash
$ systemctl restart mongod.service
$ systemctl enable mongod.service
```

2. Mistake Local DB Server Information

### 'ModuleNotFoundError: No module named "module"'

It is required to install `YARR/localdb/setting/requirements-pip.txt` to use Local DB Tools.<br>
Check the detail in the page 'administrator page'.

## Config Files Sample

### Scan Log File

**Required information**

- 'startTime' or 'timestamp'

## Database Structure

![Database Structure](images/localdb_structure.png)
