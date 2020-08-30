e.g.) chip component
```json
{
	"_id" : ObjectId("5d434f6d28a4fe3456f0c6bc"),
	"sys" : {
		"cts" : ISODate("2019-08-01T20:45:33.135Z"),
		"mts" : ISODate("2019-08-01T20:45:33.135Z"),
		"rev" : 0
	},
	"serialNumber" : "RD53A-001_chip1",
	"componentType" : "front-end_chip",
	"chipType" : "RD53A",
	"name" : "RD53A-001_chip1",
	"chipId" : 0,
	"address" : "5d434270aeeeeffb7d96892d",
	"user_id" : "5d434270aeeeeffb7d96892e",
	"children" : -1,
	"proDB" : false,
	"dbVersion" : 1
}
```

e.g.) module component
```json
{
	"_id" : ObjectId("5d434f6d28a4fe3456f0c6bb"),
	"sys" : {
		"cts" : ISODate("2019-08-01T20:45:33.134Z"),
		"mts" : ISODate("2019-08-01T20:45:33.134Z"),
		"rev" : 0
	},
	"serialNumber" : "RD53A-001",
	"componentType" : "module",
	"chipType" : "RD53A",
	"name" : "RD53A-001",
	"chipId" : -1,
	"address" : "5d434270aeeeeffb7d96892d",
	"user_id" : "5d434270aeeeeffb7d96892e",
	"children" : 1,
	"proDB" : false,
	"dbVersion" : 1
}
```

---

* `_id` : document id (unique value created by MongoDB system)
* `sys` : system information of this document
  * `rev` : the number of revision
  * `cts` : created date
  * `mts` : modified date
* `serialNumber` : the serial number of this component
* `chipType` : the asic type of the chip
* `componentType` : the type of component (e.g. "module", "front-end_chip")
* `chipId` : chip ID
* `children` : the number of children which this component has
* `address` : document id of the site where you register this component in 'institution' collection
* `user_id` : document id of the user who registered this component in 'user' collection
* `proDB` : boolean
* `dbVersion` : the version of Database
