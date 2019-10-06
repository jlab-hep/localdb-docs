e.g.)
```json
{
	"_id" : ObjectId("5cb6db418b6de04719047504"),
	"sys" : {
		"rev" : 0,
		"cts" : ISODate("2019-04-17T07:52:34.099Z"),
		"mts" : ISODate("2019-04-17T07:52:34.099Z")
	},
	"parent" : "5cb6db408b6de04719047502",
	"child" : "5cb6db418b6de04719047503",
	"chipId" : 0,
	"status" : "active",
	"dbVersion" : 1.0
}
```

---

* `_id` : document id
* `sys` : system information of this document
  * `rev` : the number of revision
  * `cts` : created date
  * `mts` : modified date
* `parent` : document id of the parent module
* `child` : document id of one of the children chips
* `chipId` : chip ID (only written in the document relating "Module" and "Front-end Chip")
* `status` : whether active or dead relationship
* `dbVersion` : the version of Database
