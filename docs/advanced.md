## MongoDB Setting

## Mongo Shell

You can use the mongo shell to query and update data.<br>
Please check [The mongo shell](https://docs.mongodb.com/manual/mongo/) to achieve more detail.

### Connect to MongoDB server

```bash
$ export PATH=$PATH:<mongodb installation dir>/bin
$ mongo [--host <IP address>] [--port <port number>]
MongoDB shell version v4.0.12
```

### Database List

```bash
$ mongo
> show dbs
admin            0.000GB
config           0.000GB
local            0.000GB
localdb          1.231GB
```

### Collection List

```bash
$ mongo
> use localdb
switched to db localdb
> show collections
childParentRelation
chip
comments
component
componentTestRun
config
environment
fs.chunks
fs.files
institution
testRun
user
```

### Document List

```bash
$ mongo
> use localdb
switched to db localdb 
> db.component.find().pretty()
{
	"_id" : ObjectId("5d66e6c54bb3d07690067816"),
	"serialNumber" : "0x044A",
}
{
	"_id" : ObjectId("5d66e6c54bb3d07690067818"),
	"serialNumber" : "0x0445",
}
Type "it" for more
```

### Query Focument

```bash
> db.component.find({ "_id": ObjectId("5d66e6c54bb3d07690067816") }).pretty()
{
	"_id" : ObjectId("5d66e6c54bb3d07690067816"),
	"serialNumber" : "0x044A",
}
``` 

