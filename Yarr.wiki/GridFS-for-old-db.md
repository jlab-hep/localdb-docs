### fs.files
e.g,)
```
{
        "_id" : ObjectId("5c13532f8591295c0062b80a"),
        "length" : NumberLong(10180),
        "chunkSize" : 261120,
        "uploadDate" : ISODate("2018-12-14T06:52:31.208Z"),
        "filename" : "pixelsensor-01_chipId2_EnMask.png"
}
```

### fs.chunks
e.g.)
```
{
        "_id" : ObjectId("5c13532f8591295c0062b80b"),
        "files_id" : ObjectId("5c13532f8591295c0062b80a"),
        "n" : 0,
        "data" : BinData(0,"iVBORw0KGgoAAAANSUhEUgAABQAAAAQACAMAAACJTQRxAAADAFB...)
}
```
About mongoDB GridFS https://docs.mongodb.com/manual/core/gridfs/