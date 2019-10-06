This page describes how to retrieve data from Local DB.

## Requirements

- DAQ Server with [required libraries installed](https://github.com/jlab-hep/Yarr/wiki/Installation)
- DB Server with [required libraries installed](https://github.com/jlab-hep/Yarr/wiki/Installation)
- Setup DAQ system: [setup_db.sh](https://github.com/jlab-hep/Yarr/wiki/Setup-DAQ-Server)

## Retrieve Tool

You can restore data from Local DB by `localdbtool-retrieve`.

### Initialize

   ```bash
   $ source ~/.local/lib/localdb/enable
   $ localdbtool-retrieve init
   ```

### Add Local DB Configuration for retrieve tool

   ```bash
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
   ```

   URL of DB Server: `mongodb://<IP address>:<port number>/`

   - IP address : IP address (or host name) of the Local DB Server
 
     It is '127.0.0.1' in the case that the Local DB Server working locally.<br>
     If you want to access the another machine remotely, set IP address or host name of the machine of the Local DB Server.

   - port number : Port number opened for the Local DB Server

     It should be '27017' in default.<br>

   URL of the Viewer Application: `http://<IP address>:<port number>/localdb/` or `http://<IP address>/localdb/`

   - IP address : IP address (or host name) of the Server where Viewer Application running
 
     It is '127.0.0.1' in the case that the Viewer Application working locally.<br>
     If you want to access the another machine remotely, set IP address or host name of the machine of the Server where Viewer Application running.

   - port number : Port number opened for the Viewer Application

     It should be '5000' in default.<br>
     It should not be needed if you access the another machine remotely.

   'connection: True/False' shows if the connection to the Local DB Server/Viewer Application is stable or unstable. <br>
   If the connection is False, you should check if Local DB Server/Viewer Application is working or if the url is correct.

### Log

   ```bash
   $ localdbtool-retrieve log
   #DB INFO# The connection of Local DB mongodb://127.0.0.1:27017/ is GOOD.
   
   test data ID: XXXXXXXXXXXXXXXXXXXXXXXX 
   User          : kubota at Tokyo_Institute_of_Technology
   Date          : 2019/07/21 03:49:37
   Serial Number : DUMMY_0
   Run Number    : 5576
   Test Type     : std_digitalscan
   DCS Data      : NULL

   <ctrl+C>
   ```
   Additional options:
   - `localdbtool-retrieve log <remote name>` : show the test data log of the 'remote name'
   - `localdbtool-retrieve log <serial number>` : show the test data of the module ('serial number')

### Fetch

   ```bash
   $ localdbtool-retrieve fetch
   #DB INFO# The connection of Local DB mongodb://atlaspc5.kek.jp:27017/ is GOOD.
   
   #DB INFO# Download Component Data of Local DB locally...
   --------------------------------------
   Component (1)
       Chip Type: FE-I4B
       Module:
           serial number: QU-09
           component type: Module
           chips: 4
       Chip (1):
           serial number: QU-09_chipId1
           component type: Front-end Chip
           chip ID: 1
       Chip (2):
           serial number: QU-09_chipId2
           component type: Front-end Chip
           chip ID: 2
       Chip (3):
           serial number: QU-09_chipId3
           component type: Front-end Chip
           chip ID: 3
       Chip (4):
           serial number: QU-09_chipId4
           component type: Front-end Chip
           chip ID: 4
   --------------------------------------
   <ctrl+C>
   ```

### Check Out

   ```bash
   $ localdbtool-retrieve checkout 
   #DB INFO# The connection of Local DB mongodb://127.0.0.1:27017/ is GOOD.

   #DB INFO# test data information
   #DB INFO# - Date          : 2019/07/21 03:49:37
   #DB INFO# - Serial Number : DUMMY_0
   #DB INFO# - Run Number    : 5576
   #DB INFO# - Test Type     : std_digitalscan
   #DB INFO# 
   #DB INFO# controller      : Found      --->   path: ./localdb-configs/controller.json
   #DB INFO# scan            : Found      --->   path: ./localdb-configs/std_digitalscan.json
   #DB INFO# chip(after)     : Found      --->   path: ./localdb-configs/chip0-chipCfg.json
   #DB INFO# connectivity    : Found      --->   path: ./localdb-configs/connectivity.json

   $ls localdb-configs/
   chip0-chipCfg.json  connectivity.json  controller.json  std_digitalscan.json
   ```
   Additional options:
   - `localdbtool-retrieve checkout <remote name>` : restore the latest test config files from the 'remote name'
   - `localdbtool-retrieve checkout <serial number>` : restore the latest test config files for 'serial number' from the 'remote name'
   - `localdbtool-retrieve checkout <test data id>` : restore the test 'test data id' config files from the 'remote name'

