You can store result data by YARR immediately following the tutorial.

### Pre Requirements

- DAQ Server with [required libraries installed](https://github.com/jlab-hep/Yarr/wiki/Installation)
- DB Server with [required libraries installed](https://github.com/jlab-hep/Yarr/wiki/Installation)

### Setup Local DB with YARR

Currently there are [another official repository for Local DB](https://gitlab.cern.ch/YARR/YARR/tree/devel) in [YARR](https://gitlab.cern.ch/YARR/YARR).<br>

```bash
$ cd YARR
$ git checkout devel
$ mkdir build
$ cd build
$ cmake3 ..
$ make -j4
$ make install
$ cd ..
```

### Setup Local DB Tools

Set Local DB default config files and tools by `setup_db.sh`.
Check the detail of `setup_db.sh` [here](https://github.com/jlab-hep/Yarr/wiki/Setup-DAQ-Server)

```bash
$ cd Yarr
$ ./localdb/setup_db.sh
[LDB] Check the exist site config...NG!

[LDB] Enter the institution name where this machine is, or 'exit' ... 
> INSTITUTION NAME
# e.g.) Tokyo Institute of Technology
# e.g.) LBNL

[LDB] Confirmation
	-----------------------
	--  Mongo DB Server  --
	-----------------------
	IP address: 127.0.0.1
	port: 27017
	-----------------
	--  Test Site  --
	-----------------
	MAC address: 18:31:bf:cc:92:b8
	Machine Name: nakedsnail.dhcp.lbl.gov
	Institution: LBNL

[LDB] Are you sure that is correct? [y/n]
> y

<lots of text>
This description is saved as ${HOME}/YARR/localdb/README
```

#### Confirmation

```bash
$ exec bash
$ source ~/.local/lib/localdb-tools/enable    # to enable tab-completion
$ localdbtool-upload init --database ~/.yarr/localdb/database.json 
#INFO# Local DB Server: mongodb://127.0.0.1:27017
#INFO# ---> connection is good.
```

### scanConsole with Local DB

You can scan with default config files and upload result data into Local DB by `scanConsole -W`

```bash
$ cd YARR
$ ./bin/scanConsole \
-r configs/controller/emuCfg.json \
-c configs/connectivity/example_fei4b_setup.json \
-s configs/scans/fei4/std_digitalscan.json \
-W
<lots of text>
#DB INFO# Local DB Server: mongodb://127.0.0.1:27017
#DB INFO# ---> connection is good.
#DB INFO# Uploading in the back ground. (log: ~/.yarr/localdb/log/)
```
Additional options:
- **-d ``<database config>``** : Set database config file (default: `${HOME}/.yarr/localdb/database.json`).
- **-u ``<user config>``** : Set user config file (default: `${HOME}/.yarr/localdb/user.json`).
- **-i ``<site config>``** : Set site config file (default: `${HOME}/.yarr/localdb/site.json`).

#### Confirmation

There are three ways to confirm the data uploaded.

1. Log File
   
   You can check if the upload is success in log file `${HOME}/.yarr/localdb/log/day.log`.
   
   ```log
   2019-07-22 18:42:23,818 - Log - INFO: -----------------------
   2019-07-22 18:42:23,820 - Log - INFO: Local DB Server: mongodb://127.0.0.1:27017
   2019-07-22 18:42:23,822 - Log - INFO: ---> connection is good.
   2019-07-22 18:42:23,822 - Log - INFO: Cache Directory: ${HOME}/YARR/data/000047_std_digitalscan/
   2019-07-22 18:42:24,050 - Log - INFO: Success
   ```

2. Retrieve Tool

   You can check uploaded test data by `localdbtool-retrieve log` in CUI

   ```bash
   $ localdbtool-retrieve init
   $ localdbtool-retrieve remote add origin
   #DB INFO# Create remote repostiory "origin"

   Enter the URL of DB Server (e.g. mongodb://127.0.0.1:27017/), or "None" if not to be set.
   mongodb://127.0.0.1:27017/

   Enter the URL of the Viewer Application (e.g. http://127.0.0.1:5000/localdb/), or "None" if not to be set.
   http://127.0.0.1:5000/localdb/

   #DB INFO#   remote: origin
   #DB INFO#   DB Server: mongodb://127.0.0.1:27017/      (connection: True)
   #DB INFO#   Viewer: http://127.0.0.1:5000/localdb/     (connection: True) 

   Are you sure that is correct? [y/n]
   y

   $ localdbtool-retrieve log
   #DB INFO# The connection of Local DB mongodb://127.0.0.1:27017/ is GOOD.
   
   test data ID: XXXXXXXXXXXXXXXXXXXXXXXX 
   User          : kubota at Tokyo_Institute_of_Technology
   Date          : 2019/07/21 03:49:37
   Serial Number : DUMMY_0
   Run Number    : 5576
   Test Type     : std_digitalscan
   DCS Data      : NULL
   ```

3. Viewer Application

   You can check uploaded test data in GUI when Viewer Application is running. <br>
   Access "http://127.0.0.1:5000/localdb/" or "http://IPaddress/localdb" in browser.
   Check the setup of 'Viewer Application' [here](https://github.com/jlab-hep/Yarr/wiki/Setup-Viewer-Application)

