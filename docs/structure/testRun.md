schema

e.g.)
```json
{
	"_id" : ObjectId("5d4343d3a223442acd80b209"),
	"sys" : {
		"cts" : ISODate("2019-08-01T19:56:03.819Z"),
		"mts" : ISODate("2019-08-01T19:56:03.819Z"),
		"rev" : 0
	},
	"exec" : "-c configs/connectivity/example_rd53a_setup.json -r configs/controller/specCfg.json -s configs/scans/rd53a/std_digitalscan.json -W ",
	"runNumber" : 163,
	"testType" : "std_digitalscan",
	"timestamp" : "2019-07-30_14:19:08",
	"startTime" : ISODate("2019-07-30T21:19:08Z"),
	"finishTime" : ISODate("2019-07-30T21:19:12Z"),
	"address" : "5d434270aeeeeffb7d96892d",
	"user_id" : "5d434270aeeeeffb7d96892e",
	"targetCharge" : -1,
	"targetTot" : -1,
	"stage" : "...",
	"chipType" : "RD53A",
	"passed" : true,
	"qcTest" : false,
	"qaTest" : false,
	"summary" : false,
	"stopwatch" : {
		"analysis" : 594,
		"config" : 36,
		"processing" : 3,
		"scan" : 2832
	},
	"environment" : "...",
	"plots" : [
		"OccupancyMap",
		"EnMask",
		"L1Dist"
	],
	"ctrlCfg" : "5d4343d3a223442acd80b20c",
	"scanCfg" : "5d4343d3a223442acd80b212",
	"dbCfg" : "5d4343d3a223442acd80b20f",
	"siteCfg" : "5d4343d3a223442acd80b210",
	"userCfg" : "5d4343d3a223442acd80b211",
	"dbVersion" : 1
}
```

---

* `_id` : document id
* `sys` : system information of this document
  * `rev` : the number of revision
  * `cts` : created date
  * `mts` : modified date
* `exec` : command line
* `runNumber` : the run number of this test
* `testType` : the name of this test
* `timestamp` : timestamp
* `startTime` : start time of the test
* `finishTime` : finish time of the test
* `address` : document id of the production site in 'institution' collection
* `user_id` : document id of the user in 'user' collection
* `targetCharge` : the target of the charge in tuning
* `targetTot` : the target of the ToT in tuning
* `stage` : the process stage
* `chipType` : asic type
* `passed` : boolean
* `qcTest` : boolean
* `qaTest` : boolean
* `summary` : boolean
* `stopwatch` : 
* `environment` : document id of the environment data in 'environment' collection
* `plots` : names of output plots after scan
* `ctrlCfg` : controller config id (document id in 'config' collection)
* `scanCfg`: scan config id (document id in 'config' collection)
* `dbCfg` : database config id (document id in 'config' collection)
* `siteCfg` : site config id (document id in 'config' collection)
* `userCfg` : user config id (document id in 'config' collection)
* `dbVersion` : the version of Database
