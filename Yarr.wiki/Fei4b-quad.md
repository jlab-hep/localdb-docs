After step in [Quick tutorial](https://github.com/jlab-hep/Yarr/wiki/Quick-tutorial-for-Yarr).

## 2) Ready
   * `Yarr/src/configs/create_fei4b_4chip_config.sh` : To create connectivity and 4 chip configs and write component data into database.

     Change 'tx_fix', 'rx_start' in `Yarr/src/configs/create_fei4b_4chip_config.sh` as your YARR HW setup.

     create_fei4b_4chip_config.sh )
     ```
     #!/bin/sh
     
     # Change fixed tx channel and rx start channel
     tx_fix=4      <--- change number as your setup
     rx_start=4    <--- change number as your setup
     ```

     Default setup is 'tx_fix = 4' and 'rx_start = 4'.

## 3) Scan 
1) Create connectivity for DB

   First, create a connectivity and configs. 
   
   usage)
   ```
   $ cd Yarr/src/configs
   $ ./create_fei4b_4chip_config.sh 'module-serial-number' testRunInfo.json
   Write Database ... [ serial number: 'module-serial-number', environmental configuration: testRunInfo.json ]
   Continue ... [y/n] y ---> create config files and write database
   ```

   e.g.)
   ```
   $ cd Yarr/src/configs
   $ ./create_fei4b_4chip_config.sh KEK-777 testRunInfo.json
   Write Database ... [ serial number: KEK-777, environmental configuration: testRunInfo.json ]
   Continue ... [y/n] y
   Create KEK-777_fei4b_chipId1.json.
   Create KEK-777_fei4b_chipId2.json.
   Create KEK-777_fei4b_chipId3.json.
   Create KEK-777_fei4b_chipId4.json.
   Create KEK-777_fei4module.json.
   ./bin/dbRegisterComponent -c configs/connectivity/KEK-777_fei4module.json
   $ 
   ```

   The connectivity config (serialNumber of module and 4 FEI4B chips) and the chip configs (chip name) will be created as follows:
   
   * `Yarr/src/configs/connectivity/KEK-777_fei4module.json`
   * `Yarr/src/configs/KEK-777_fei4b_chipId1.json` contains `"name": "<module-serialNumber>_chipId1.json", "rxChannel': 4, 'txChannel': 4`
   * `Yarr/src/configs/KEK-777_fei4b_chipId2.json` contains `"name": "<module-serialNumber>_chipId1.json", "rxChannel': 5, 'txChannel': 4`
   * `Yarr/src/configs/KEK-777_fei4b_chipId3.json` contains `"name": "<module-serialNumber>_chipId1.json", "rxChannel': 6, 'txChannel': 4`
   * `Yarr/src/configs/KEK-777_fei4b_chipId4.json` contains `"name": "<module-serialNumber>_chipId1.json", "rxChannel': 7, 'txChannel': 4`

   At the same time, component information are written into database.
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
	"serialNumber" : "KEK-777_chipId1",
	"componentType" : "FE-I4B",
	"name" : "KEK-777_chipId1",
	"institution" : "Abc_University",
	"userIdentity" : "FirstName_LastName"
   }
   {
	"_id" : ObjectId("002"),
	"serialNumber" : "KEK-777_chipId2",
	"componentType" : "FE-I4B",
	"name" : "KEK-777_chipId2",
	"institution" : "Abc_University",
	"userIdentity" : "FirstName_LastName"
   }
   {
	"_id" : ObjectId("003"),
	"serialNumber" : "KEK-777_chipId3",
	"componentType" : "FE-I4B",
	"name" : "KEK-777_chipId3",
	"institution" : "Abc_University",
	"userIdentity" : "FirstName_LastName"
   }
   {
	"_id" : ObjectId("004"),
	"serialNumber" : "KEK-777_chipId4",
	"componentType" : "FE-I4B",
	"name" : "KEK-777_chipId4",
	"institution" : "Abc_University",
	"userIdentity" : "FirstName_LastName"
   }
   {
	"_id" : ObjectId("005"),
	"serialNumber" : "KEK-777",
	"componentType" : "Module",
	"institution" : "Abc_University",
	"userIdentity" : "FirstName_LastName"
   }
   ```

2) Do a scan
   * `Yarr/src/doScan.sh` : To run a single scan.

     ```
     $ ./doScan.sh 'module-serial-number' 'scan-type' 
     ```

     For example,
     ```
     $ cd Yarr/src
     $ ./doScan.sh KEK-777 digitalscan
     ```

   * `Yarr/src/doEverything.sh` : To run all scans. (QA)

     ```
     $ ./doEverything.sh 'module-serial-number'
     ```

     For example,
     ```
     $ cd Yarr/src
     $ ./create_fei4b_4chip_config.sh KEK-777
     ```
