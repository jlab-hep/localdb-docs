e.g.) chip component
```
{
        "_id" : ObjectId("5c134e988591292d277935f5"),
        "sys" : {
                "rev" : 0,
                "cts" : ISODate("2018-12-14T06:32:56.655Z"),
                "mts" : ISODate("2018-12-14T06:32:56.655Z")
        },
        "serialNumber" : "kek-114_chipId4",
        "componentType" : "FE-I4B",
        "name" : "kek-114_chipId4",
        "institution" : "obsidian",
        "userIdentity" : "eunchong"
}
```

e.g.) module component
```
{
        "_id" : ObjectId("5c134e988591292d277935f6"),
        "sys" : {
                "rev" : 0,
                "cts" : ISODate("2018-12-14T06:32:56.657Z"),
                "mts" : ISODate("2018-12-14T06:32:56.657Z")
        },
        "serialNumber" : "kek-114",
        "componentType" : "Module",
        "institution" : "obsidian",
        "userIdentity" : "eunchong"
}
```

---

* `_id` : document id
* `sys` : system information of this document
  * `rev` : the number of revision
  * `cts` : created date
  * `mts` : modified date
* `serialNumber` : the serial number of this component
* `componentType` : the asic type of the chip, or "Module"
* `name`: 
* `institution` : shifter's institution
* `userIdentity` : shifter's name
