### fs.files
e.g,)
```json
{
	"_id" : ObjectId("5cb6db928b6de04a4a3217a5"),
	"length" : NumberLong(287),
	"chunkSize" : 261120,
	"uploadDate" : ISODate("2019-04-17T07:53:56.142Z"),
	"filename" : "controller.json",
	"dbVersion" : 0.9,
	"hash" : "34d1f52eab9b1f754d9594b698992a782b865499"
}
```

* `_id` : document id
* `length`
* `chunkSize`
* `uploadDate`
* `filename`
* `dbVersion` :  the version of Database
* `hash` : hash value of this data (written in only config files)

### fs.chunks
e.g.)
```json
{
        "_id" : ObjectId("5c13532f8591295c0062b80b"),
        "files_id" : ObjectId("5cb6db928b6de04a4a3217a5"),
        "n" : 0,
        "data" : BinData(0,"iVBORw0KGgoAAAANSUhEUgAABQAAAAQACAMAAACJTQRxAAADAFB...)
}
```

* `_id` : document id
* `files_id` : file id (document id in fs.files)
* `n`
* `data`
* `dbVersion` :  the version of Database


About mongoDB GridFS https://docs.mongodb.com/manual/core/gridfs/
