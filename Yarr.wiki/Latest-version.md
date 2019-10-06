After step in [Quick tutorial](https://github.com/jlab-hep/Yarr/wiki/Quick-tutorial-for-Yarr).

## 2) Create config files
### 1) Ready
   * `Yarr/src/configs/create_config.sh`: To create config files and write component data into database.

     Change 'tx_fix', 'rx_start' in `Yarr/src/configs/create_config.sh` as your YARR HW setup.

     create_fei4b_4chip_config.sh )
     ```
     #!/bin/bash
     
     # Change fixed tx channel and rx start channel
     tx_fix=0      <--- change number as your setup
     rx_start=0    <--- change number as your setup
     ```

     Default setup is 'tx_fix = 0' and 'rx_start = 0'.

### 2) Config creation
   * `Yarr/src/configs/create_config.sh` can make config file set (config, connectivity config, controller config, and user config)

     usage)
     ```
     $ cd Yarr/src/configs
     $ ./create_config.sh -a 'rd53a/fei4b' -m 'module-serial-number' -i 'path-to-userCfg' -c 'number of chips’
     e.g.) ./create_config.sh -a rd53a -m ABC-001 -i testRunInfo.json -c 4
     Create config directory rd53a/ABC-001
     Create controller.json    <--- copied from controller/specCfg.json
     Create info.json          <--- copied from user config in path-to-userCfg
     Create connectivity.json
     Create chipId1.json 
     Create chipId2.json
     Create chipId3.json
     Create chipId4.json
     ```

     config files)
     ```
     <src/configs>
       |--- <rd53a or fei4b>
              |--- <serial number>
                       |--- chipId#.json      : config file for chip
                       |--- connectivity.json : connectivity config file
                       |--- controller.json   : controller config file (default is copied from specCfg.json)
                       |--- info.json         : user config file
                       |--- <backup>          : backup directory
     ```

     connectivity.json)
     ```
     {
         "module": {
             "serialNumber": "'module-serial-number'",
             "componentType": "Module"
         },
         "chipType": "RD53A",
         "chips": [
             {
                 "serialNumber": "'module-serial-number'_chipId1",
                 "componentType": "Front-end Chip",
                 "config": "configs/rd53a/'module-serial-number'/chipId1.json",
                 "tx": 'tx_fix',
                 "rx": 'rx_start'
             },
             {
                 "serialNumber": "'module-serial-number'_chipId2",
                 "componentType": "Front-end Chip",
                 "config": "configs/rd53a/'module-serial-number'/chipId2.json",
                 "tx": 'tx_fix',
                 "rx": 'rx_start'+1
             },
             {
                 "serialNumber": "'module-serial-number'_chipId3",
                 "componentType": "Front-end Chip",
                 "config": "configs/rd53a/'module-serial-number'/chipId3.json",
                 "tx": 'tx_fix',
                 "rx": 'rx_start'+2
             },
             {
                 "serialNumber": "'module-serial-number'_chipId4",
                 "componentType": "Front-end Chip",
                 "config": "configs/rd53a/'module-serial-number'/chipId4.json",
                 "tx": 'tx_fix',
                 "rx": 'rx_start'+3
             }
         ]
     }
     ```
     chipId#.json is copied from default_<asic>.json and changed chipId and name:
     ```
     {
         "ASIC": {
             "Parameter": {
                 "ChipId": #,
                 "Name": "chipId#",
             },
         }
     }
     ```
   ** `./create_config.sh -r 'path-to-controller'` can specify the controller config

     usage)
     ```
     $ cd Yarr/src/configs
     $ ./create_config.sh -a 'rd53a/fei4b' -m 'module-serial-number' -i 'path-to-userCfg' -c 'number of chips’ -r 'path-to-controllerCfg'
     e.g.) ./create_config.sh -a rd53a -m ABC-001 -i testRunInfo.json -c 4 -r controller/emuCfg.json
     Create config directory rd53a/ABC-001
     Create controller.json    <--- copied from controller/emuCfg.json
     Create info.json          <--- copied from user config in path-to-userCfg
     ```

   ** `./create_config.sh -d` can write component information into database after config creation

     usage)
     ```
     $ cd Yarr/src/configs
     $ ./create_config.sh -a 'rd53a/fei4b' -m 'module-serial-number' -i 'path-to-userCfg' -c 'number of chips’ -d
     e.g.) ./create_config.sh -a rd53a -m ABC-001 -i testRunInfo.json -c 4 -d
     ```
     And you can check it in terminal as following:
     ```
     $ mongo
     MongoDB shell version v3.6.8
     connecting to: mongodb://127.0.0.1:28000/
     MongoDB server version: 3.6.8
     > use yarrdb
     switched to db yarrdb
     > db.component.find().pretty()
     {
        "_id" : ObjectId("001"),
        "serialNumber" : "'module-serial-number'_chipId1",
        "componentType" : "RD53A/FE-I4B",
        "name" : "chipId1",
        "institution" : "Abc_University",
        "userIdentity" : "FirstName_LastName"
     }
     {
        "_id" : ObjectId("005"),
        "serialNumber" : "'module-serial-number'",
        "componentType" : "Module",
        "institution" : "Abc_University",
        "userIdentity" : "FirstName_LastName"
     }
     ```
   ** `./create_config.sh` can reset config files based on connectivity.json exist

     usage)
     ```
     $ cd Yarr/src/configs
     $ ./create_config.sh -a 'rd53a/fei4b' -m 'module-serial-number'
     e.g.) ./create_config.sh -a rd53a -m ABC-001
     Config files of ABC-001 are already exist, then move it to backup directory
     ( Create info.json          <--- reset user config if you specify new one with '-i' )
     ( Create controller.json    <--- reset controller config if you specify new one with '-r' )
     Reset chipId#.json         <--- chipId and name refers to original config
     ```
   ** `./create_config.sh -R` can recreate config files (reset all config files and settings)

     usage)
     ```
     $ cd Yarr/src/configs
     $ ./create_config.sh -a 'rd53a/fei4b' -m 'module-serial-number' -R
     e.g.) ./create_config.sh -a rd53a -m ABC-001 -R
     Reset config files of ABC-001
     Move config files to backup directory before reset
     Continue to remake config files ... [y/n]    <--- you can continue to create configs with "-i 'path-to-userCfg' -c 'number of chips’"
     ```

## 3) Do a scan
   * Basic command: scanConsole with uploading database

     ```
     $ ./bin/scanConsole -r <controller> -c <connectivity> -s <scan> -p -W -I <environment info> # for both of rd53a and fei4b
     e.g.) 
     # fei4b
     $ ./bin/scanConsole -r configs/fei4b/KEK-777/controller.json -c configs/fei4b/KEK-777/connectivity.json -s digitalscan -p -W -I configs/fei4b/KEK-777/info.json 
     # rd53a
     $ ./bin/scanConsole -r configs/rd53a/KEK-777/controller.json -c configs/rd53a/KEK-777/connectivity.json -s configs/scans/rd53a/std_digitalscan.json -p -W -I configs/rd53a/KEK-777/info.json
     ``` 

## 4) Useful scripts

   * `Yarr/src/doScan_fei4b.sh` : To run a single scan for fei4b

     ```
     $ ./doScan_fei4b.sh -m 'module-serial-number' -s 'scan-type' [-r ControllerCfg] [-n ConnectivityCfg] [-i EnvironmentCfg] [-c TargetCharge] [-t TargetTot] [-p TargetPreamp] [-M mask] [-d] [-l]
     ```

     For example after creating config file with `create_config.sh`,
     ```
     $ cd Yarr/src
     $ ./doScan_fei4b.sh -m KEK-777 -s digitalscan    # not upload into database
     ---> this can run: ./bin/scanConsole -r configs/fei4b/KEK-777/controller.json -c configs/fei4b/KEK-777/connectivity.json -s digitalscan -p -m -1
     $ ./doScan_fei4b.sh -m KEK-777 -s digitalscan -d # upload into database
     ---> this can run: ./bin/scanConsole -r configs/fei4b/KEK-777/controller.json -c configs/fei4b/KEK-777/connectivity.json -s digitalscan -p -m -1 -W -I configs/fei4b/KEK-777/info.json
     ```

   * `Yarr/src/doScan_rd53a.sh` : To run a single scan for rd53a

     ```
     $ ./doScan_rd53a.sh -m 'module-serial-number' -s 'scan-type' [-r ControllerCfg] [-n ConnectivityCfg] [-i EnvironmentCfg] [-c TargetCharge] [-t TargetTot] [-p TargetPreamp] [-M mask] [-d] [-l]
     ```

     For example after creating config file with `create_config.sh`,
     ```
     $ cd Yarr/src
     $ ./doScan_rd53a.sh -m ABC-001 -s digitalscan    # not upload into database
     ---> this can run: ./bin/scanConsole -r configs/rd53a/ABC-001/controller.json -c configs/rd53a/ABC-001/connectivity.json -s digitalscan -p -m -1
     $ ./doScan_rd53a.sh -m ABC-001 -s digitalscan -d # upload into database
     ---> this can run: ./bin/scanConsole -r configs/rd53a/ABC-001/controller.json -c configs/rd53a/ABC-001/connectivity.json -s digitalscan -p -m -1 -W -I configs/rd53a/ABC-001/info.json
     ```

   * `Yarr/src/doEverything.sh` : To run all scans. (QA)

     ```
     $ ./doEverything.sh -a fei4b -m 'module-serial-number'    # not upload into database
     $ ./doEverything.sh -a fei4b -m 'module-serial-number' -d # upload into database
     ```

     For example,
     ```
     $ cd Yarr/src
     $ ./doEverything.sh -a fei4b -m KEK-777 -d
     ```
