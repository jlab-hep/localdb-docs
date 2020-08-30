e.g.) 
```json
{
	"_id" : ObjectId("5d3a3d8dcf401b22f5d9b6c6"),
	"sys" : {
		"cts" : ISODate("2019-07-25T23:38:53.612Z"),
		"mts" : ISODate("2019-07-25T23:38:53.612Z"),
		"rev" : 0
	},
	"address" : "XX:XX:XX:XX:XX:XX",
	"institution" : "Tokyo_Institute_of_Technology",
        "hostname" : "lazulite",
	"dbVersion" : 1
}
```

---

* `_id` : document id
* `sys` : system information of this document
  * `rev` : the number of revision
  * `cts` : created date
  * `mts` : modified date
* `address` : MAC address of the machine
* `institution` : the name of institution
* `hostname` : hostname/name of the machine
* `dbVersion` :  the version of Database
