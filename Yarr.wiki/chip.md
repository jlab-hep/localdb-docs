```json
{
	"_id" : ObjectId("5d434398aa1d05a330d6b851"),
	"sys" : {
		"cts" : ISODate("2019-08-01T19:55:04.087Z"),
		"mts" : ISODate("2019-08-01T19:55:04.087Z"),
		"rev" : 0
	},
	"name" : "FEI4B-001_chip1",
	"chipId" : 1,
	"chipType" : "FE-I4B",
	"componentType" : "front-end_chip",
	"dbVersion" : 1
}
```

---

* `_id` : document id (unique value created by MongoDB system)
* `sys` : system information of this document
  * `rev` : the number of revision
  * `cts` : created date
  * `mts` : modified date
* `name` : the name of this chip (should be serial number)
* `chipId` : chip ID
* `chipType` : the asic type of the chip
* `componentType` : the type of component ("front-end_chip")
* `dbVersion` : the version of Database
