schema

e.g.)
```
{
        "_id" : ObjectId("5c13532f8591295c0062b803"),
        "sys" : {
                "rev" : 0,
                "cts" : ISODate("2018-12-14T06:52:31.193Z"),
                "mts" : ISODate("2018-12-14T06:52:31.193Z")
        },
        "testType" : "analogscan",
        "runNumber" : 792,
        "date" : ISODate("2018-12-14T06:52:31.193Z"),
        "institution" : "Kyushu_University",
        "userIdentity" : "Shuichi_Fujino",
        "passed" : true,
        "problems" : true,
        "state" : "ready",
        "comments" : [ ],
        "attachments" : [
                {
                        "code" : "5c13532f8591295c0062b805",
                        "dateTime" : ISODate("2018-12-14T06:52:31.204Z"),
                        "title" : "title",
                        "description" : "describe",
                        "contentType" : "after",
                        "filename" : "pixelsensor-01_chipId2.json"
                },
                {
                        "code" : "5c13532f8591295c0062b808",
                        "dateTime" : ISODate("2018-12-14T06:52:31.206Z"),
                        "title" : "title",
                        "description" : "describe",
                        "contentType" : "dat",
                        "filename" : "pixelsensor-01_chipId2_EnMask"
                },
                {
                        "code" : "5c13532f8591295c0062b80a",
                        "dateTime" : ISODate("2018-12-14T06:52:31.208Z"),
                        "title" : "title",
                        "description" : "describe",
                        "contentType" : "png",
                        "filename" : "pixelsensor-01_chipId2_EnMask"
                },
                {
                        "code" : "5c13532f8591295c0062b80c",
                        "dateTime" : ISODate("2018-12-14T06:52:31.210Z"),
                        "title" : "title",
                        "description" : "describe",
                        "contentType" : "dat",
                        "filename" : "pixelsensor-01_chipId2_L1Dist"
                },
                {
                        "code" : "5c13532f8591295c0062b80e",
                        "dateTime" : ISODate("2018-12-14T06:52:31.212Z"),
                        "title" : "title",
                        "description" : "describe",
                        "contentType" : "pdf",
                        "filename" : "pixelsensor-01_chipId2_L1Dist"
                },
                {
                        "code" : "5c13532f8591295c0062b810",
                        "dateTime" : ISODate("2018-12-14T06:52:31.214Z"),
                        "title" : "title",
                        "description" : "describe",
                        "contentType" : "dat",
                        "filename" : "pixelsensor-01_chipId2_OccupancyMap"
                },
                {
                        "code" : "5c13532f8591295c0062b812",
                        "dateTime" : ISODate("2018-12-14T06:52:31.215Z"),
                        "title" : "title",
                        "description" : "describe",
                        "contentType" : "png",
                        "filename" : "pixelsensor-01_chipId2_OccupancyMap"
                }
        ],
        "defects" : [ ],
        "display" : false
}
```

---

* `_id` : document id
* `sys` : system information of this document
  * `rev` : the number of revision
  * `cts` : created date
  * `mts` : modified date
* `testType` : the name of this test
* `runNumber` : the run number of this test
* `date` : tested date
* `institution` : shifter's institution
* `userIdentity` : shifter's name
* `passed`
* `problems`
* `state`
* `comments` : comments about this test
* `attachments` : the output data of Yarr in this test
  * `code` : data id (document id in fs.files)
  * `dateTime` : uploaded date
  * `title`
  * `description`
  * `contentType` : the format of this data
  * `filename` : the name of this data
* `defects`
* `display` : boolean about representing ( true : this test is represented )