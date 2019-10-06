e.g.) 
```json
{
	"_id" : ObjectId("5cb6dace8b6de042ef053b72"),
	"sys" : {
		"rev" : 0,
		"cts" : ISODate("2019-04-17T07:50:39.122Z"),
		"mts" : ISODate("2019-04-17T07:50:39.122Z")
	},
	"userName" : "arisa_kubota",
	"institution" : "tokyo_institute_of_technology",
        "description" : "default",
        "USER" : "akubata",
        "HOSTNAME" : "lazulite",
	"userType" : "readWrite",
	"dbVersion" : 1.0
}
```

---

* `_id` : document id
* `sys` : system information of this document
  * `rev` : the number of revision
  * `cts` : created date
  * `mts` : modified date
* `userName` : the name of this user (<first name>_<last name>)
* `institution` : the name of institution where user belongs
* `description` : specefic description of this user
* `USER` : the user account name of the machine
* `HOSTNAME` : the hostname of the machine
* `userType` : the authority of this user
* `dbVersion` :  the version of Database
