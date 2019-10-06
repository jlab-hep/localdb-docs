After starting mongo server, you can access database using mongo shell.
* ref1) [install and start mongo server](https://github.com/jlab-hep/Yarr/wiki/Install-and-start-server)
* ref2) [Data schema](https://github.com/jlab-hep/Yarr/wiki/Data-schema)

## 1) Start mongo shell
```
$ mongo
MongoDB shell version v3.6.8
connecting to: mongodb://127.0.0.1:28000/
MongoDB server version: 3.6.8
> 
```

## 2) Select Database
```
> show dbs             # list the available databases
admin   0.000GB
config  0.000GB
local   0.000GB
yarrdb  0.973GB
> use yarrdb           # select database
switched to db yarrdb  
>
```

## 3) Check contents of database
```
> show collections     # list of all collections for current database
childParentRelation
component
componentTestRun
fs.chunks
fs.files
testRun
> db.component.find().pretty()    # show documents in a collection
{
	"_id" : ObjectId("###"),
        # document
}
>
```

## 4) Query document
```
> db.component.find({ "_id" : "001" }).pretty() # specify selection filter
{
	"_id" : ObjectId("001"),
        # document
}
>
``` 