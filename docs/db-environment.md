e.g.) 
```json
{
	"_id" : ObjectId("5d3a4dfec4110ac3a1ef2bcf"),
	"dbVersion" : 1,
	"sys" : {
		"cts" : ISODate("2019-07-26T00:49:02.506Z"),
		"mts" : ISODate("2019-07-26T00:49:02.506Z"),
		"rev" : 0
	},
	"vddd_voltage" : [
		{
			"data" : [
				{
					"date" : ISODate("2019-06-24T11:49:13Z"),
					"value" : 10
				},
				{
					"date" : ISODate("2019-06-24T11:49:23Z"),
					"value" : 11
				},
				{
					"date" : ISODate("2019-06-24T11:49:33Z"),
					"value" : 12
				},
				{
					"date" : ISODate("2019-06-24T11:49:43Z"),
					"value" : 13
				},
			],
			"description" : "VDDD Voltage [V]",
			"mode" : "null",
			"setting" : "10",
			"num" : 0
		}
	]
}
```

---

* `_id` : document id
* `sys` : system information of this document
  * `rev` : the number of revision
  * `cts` : created date
  * `mts` : modified date
* `"DCS KEY"` : DCS keyword written in database config file
  * `data` : sets of `date` and `value`
    * `date` : datetime
    * `value` : DCS data value
  * `description` : description of DCS data
  * `mode` : DCS setting mode
  * `setting` : DCS setting value
  * `num` : DCS key number (the combination of "key" and "num" specifies which data in the DCS data file)
