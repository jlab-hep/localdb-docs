This page describes how to use scanConsole with Local DB.

## scanConsole (general)

### Requirements

- DAQ Server with [required libraries installed](https://github.com/jlab-hep/Yarr/wiki/Installation)
- DB Server with [required libraries installed](https://github.com/jlab-hep/Yarr/wiki/Installation)
- Setup DAQ system: [setup_db.sh](https://github.com/jlab-hep/Yarr/wiki/Setup-DAQ-Server)
- Compile scanConsole 

```bash
$ cd YARR
$ git checkout devel
$ mkdir build-localdb
$ cd build-localdb
$ cmake3 ../
$ make -j4
$ make install
```

### Scan 

```bash
$ bin/scanConsole \
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

You can confirm the data uploaded by:
- Log file in `${HOME}/.yarr/localdb/log/day.log`
- [Retrieve Tool](https://github.com/jlab-hep/Yarr/wiki/Retrieve)
- [Viewer Application](https://github.com/jlab-hep/Yarr/wiki/Viewer)

## scanConsole with registered Module

### Additional Requirements

Connecivity config file should be prepared properly.

- connectivity config (json)

   **Required information**
   - stage: the test stage for the module, should be selected from the stage list written in [database.json](https://github.com/jlab-hep/Yarr/wiki/database-config-file)
   - module.serialNumber: serial number of the module
   - chipType: "FEI4B" or "RD53A"
   - chips: chips on the module
     - chips.i.serialNumber: serial number of the chip
     - chips.i.config: path to chip config file
     - chips.i.tx: must be "int"
     - chips.i.rx: must be "int"
 
   <details><summary>connectivity.json for RD53A</summary><div>
 
   ```json
   {
       "stage": "Testing",
       "module": {
           "serialNumber": "RD53A-001"
       },
       "chipType" : "RD53A",
       "chips" : [
           {
               "serialNumber": "RD53A-001_chip1",
               "config" : "configs/defaults/default_rd53a.json",
               "tx" : 0,
               "rx" : 0
           }
       ]
   }
   ```
 
   </div></details>
 
   <details><summary>connectivity.json for FEI4B</summary><div>
 
   ```json
   {
       "stage": "Testing",
       "module": {
           "serialNumber": "FEI4B-001"
       },
       "chipType" : "FEI4B",
       "chips" : [
           {
               "serialNumber": "FEI4B-001-chip1",
               "config" : "configs/chip1.json",
               "tx" : 0,
               "rx" : 0
           },
           {
               "serialNumber": "FEI4B-001-chip2",
               "config" : "configs/chip2.json",
               "tx" : 0,
               "rx" : 1
           },
           {
               "serialNumber": "FEI4B-001-chip3",
               "config" : "configs/chip3.json",
               "tx" : 0,
               "rx" : 2
           },
           {
               "serialNumber": "FEI4B-001-chip4",
               "config" : "configs/chip4.json",
               "tx" : 0,
               "rx" : 3
           }
       ]
   }
   ```
 
   </div></details>

### Scan

```bash
$ ./bin/scanConsole \
-r configs/controller/emuCfg.json \
-c configs/connectivity.json \
-s configs/scans/fei4/std_digitalscan.json \
-W \
-u user.json
<Lots of text>
#DB INFO# Local DB Server: mongodb://127.0.0.1:27017
#DB INFO# ---> connection is good.
#DB INFO# Uploading in the back ground. (log: ~/.yarr/localdb/log/)
```

