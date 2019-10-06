e.g.) 
```json
{
	"_id" : ObjectId("5d434270aeeeeffb7d968931"),
	"sys" : {
		"mts" : ISODate("2019-08-01T19:51:46.917Z"),
		"rev" : 1
	},
	"component" : "...",
	"testRun" : "5d434270aeeeeffb7d968930",
	"chip" : "5d434270aeeeeffb7d96892f",
        "name" : "JohnDoe_1",
	"config" : "rd53a_test.json",
	"enable" : 1,
	"locked" : 0,
	"rx" : 0,
	"tx" : 0,
	"geomId" : 0,
	"attachments" : [
		{
			"code" : "5d4342d3aa3e9a2c43ec77a0",
			"dateTime" : ISODate("2019-08-01T19:51:47.095Z"),
			"title" : "EnMask",
			"description" : "describe",
			"contentType" : "dat",
			"filename" : "EnMask.dat"
		},
		{
			"code" : "5d4342d3aa3e9a2c43ec77a2",
			"dateTime" : ISODate("2019-08-01T19:51:47.099Z"),
			"title" : "OccupancyMap",
			"description" : "describe",
			"contentType" : "dat",
			"filename" : "OccupancyMap.dat"
		},
		{
			"code" : "5d4342d3aa3e9a2c43ec77a5",
			"dateTime" : ISODate("2019-08-01T19:51:47.102Z"),
			"title" : "L1Dist",
			"description" : "describe",
			"contentType" : "dat",
			"filename" : "L1Dist.dat"
		}
	],
	"beforeCfg" : "5d4342d2aa3e9a2c43ec779e",
	"afterCfg" : "5d4342d3aa3e9a2c43ec779f",
	"dbVersion" : 1
}
```

---

* `_id` : document id
* `sys` : system information of this document
  * `rev` : the number of revision
  * `cts` : created date
  * `mts` : modified date
* `component` : document id of this chip in 'componentTestRun' collection
* `testRun` : document id of this test in 'testRun' collection
* `chip` : document id of this chip in 'chip' collection
* `name` : the name of this chip (should be serialNumber)
* `chipId` : chip ID
* `geomId` : geometorical ID (If not specified, the order written in the connectivity)
* `tx` : tx channel of this component in this test
* `rx` : rx channel of this component in this test
* `config` : the name of the chip config file
* `attachments` : the output data of Yarr in this test
  * `code` : data id (document id in fs.files)
  * `dateTime` : uploaded date
  * `title` : title of the plot
  * `description`
  * `contentType` : the format of this data
  * `filename` : the name of this data
* `beforeCfg` : chip config (before the test) id (document id in 'config' collection)
* `afterCfg` : chip config (after the test) id (document id in 'config' collection)
* `dbVersion` :  the version of Database

