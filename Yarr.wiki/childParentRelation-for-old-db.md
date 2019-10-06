e.g.)
```
{
        "_id" : ObjectId("5c134b5385912906a81ebf9a"),
        "sys" : {
                "rev" : 0,
                "cts" : ISODate("2018-12-14T06:18:59.042Z"),
                "mts" : ISODate("2018-12-14T06:18:59.042Z")
        },
        "parent" : "5c134b5385912906a81ebf96",
        "child" : "5c134b5385912906a81ebf95"
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