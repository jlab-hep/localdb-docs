## Convert DB Structure

0. Make a back-up of current Local DB

See [Archive Tool](../tool/archive.md) to make an archive of Local DB, or just execute the sudo command:

```bash
$ sudo systemctl stop mongod.service
$ date=`date +"%y%m%d"`
$ sudo tar zcvf mongo-${date}.tar.gz /var/lib/mongo
$ sudo systemctl restart mongod.service
```

1. Convert DB

`localdb-tools/scripts/tools/make_convert.py` can convert the structure of DB from old one to new one.<br>
Modify the DB setting in following part of `make_convert.py` if needed:

```python
### Set DBs
url = 'mongodb://127.0.0.1:27017'
client = MongoClient( url )
new_db = 'localdb'          # New Local DB (default. localdb)
copy_db = 'localdb_replica' # Replica of the old Local DB (default. localdb_replica)
old_db  = 'yarrdb'          # Old YARR DB (default. yarrdb)
```

And run it:

```bash
$ cd localDB-tools/scripts/tools
$ python3 make_covert.py
# Continue to convert DB: yarrdb/localdb(old) ---> localdb(latest)? (y/n) > y

# Update database scheme: localdb
	2019-10-15T08:11:01 [Start]
  <some texts>
	# Succeeded in Update

# Convert database scheme: yarrdb -> localdb
	2019-10-15T08:11:01 [Start]
  <some texts>
	# Succeeded in Conversion

# Verify database scheme: localdb
	2019-10-15T08:33:52 [Start]
  <some texts>
	# Succeeded in Verification

  <some texts>
	# Succeeded in All Steps
```

It takes about 30 minutes for 1GB data size to complete the conversion. <br>
You can run `make_conver.py` again to restore the replica of DB and start over.
