e.g.) 
```json
{
	"_id" : ObjectId("5cb6dedb8b6de0667e48d5ae"),
	"sys" : {
		"rev" : 0,
		"cts" : ISODate("2019-04-17T08:07:55.710Z"),
		"mts" : ISODate("2019-04-17T08:07:55.710Z")
	},
	"filename" : "afterCfg.json",
	"chipType" : "RD53A",
	"title" : "chipCfg",
	"format" : "fs.files",
	"data_id" : "5cb6dedb8b6de0667e48d5aa",
	"dbVersion" : 1
}
```

---

* `_id` : document id
* `sys` : system information of this document
  * `rev` : the number of revision
  * `cts` : created date
  * `mts` : modified date
* `filename` : the name of this config file
* `chipType` : the asic type of the chip
* `title` : the title of this config file
* `format` : upload format (collection name)
* `data_id` : data id (document id in collection written at `format`)
* `dbVersion` : the version of Database
