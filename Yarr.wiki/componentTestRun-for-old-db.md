e.g.) 
```
{
        "_id" : ObjectId("5c1352ea85912959572dbd77"),
        "sys" : {
                "rev" : 0,
                "cts" : ISODate("2018-12-14T06:51:22.056Z"),
                "mts" : ISODate("2018-12-14T06:51:22.056Z")
        },
        "component" : "5c134b5385912906a81ebf95",
        "state" : "...",
        "stage" : "encapsulation",
        "testType" : "digitalscan",
        "testRun" : "5c1352ea85912959572dbd76",
        "qaTest" : false,
        "runNumber" : 791,
        "passed" : true,
        "problems" : true,
        "environments" : [
                {
                        "key" : "hv",
                        "value" : "-80",
                        "description" : "High voltage [V]"
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
* `component` : document id of the component tested
* `state` : 
* `stage` : the process stage
* `testType` : the name of this test
* `testRun` : document id of this test
* `qaTest` : 
* `runNumber` : the run number of this test
* `passed` : 
* `problems` : 
* `environments` : environment information of this test
  * `key` : key word of the environment item
  * `description` : the environment item
  * `value` : the value of the environment item
