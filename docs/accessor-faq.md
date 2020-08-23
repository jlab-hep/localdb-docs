## Error and Exit Messages

- [Not found xxx](#not-found-xxx)
- [Coult not parse xxx](#could-not-parse-xxx)

### Not found xxx

##### Not found database config

**example**

```bash
$./bin/dbAccessor -N -d database.json
[  info  ]: DBHandler: Check DB Connection
[  info  ]: ------------------------------
[  info  ]: Function: Initialize upload function and check connection to Local DB
[  info  ]: -> Setting database config: /home/example/YARR/database.json
[ error  ]: Not found database config.
[ error  ]: Specify the correct path to database config file under -d option.
[  info  ]: ------------------------------
```

**problem**

The [dbAccessor](accessor.md) cannot find the existence of the database config file in the specified path.

**solution**

1. Make sure the database config file exists at the specified path.
2. Make sure the specified path is to a file, not a directory.
3. Make sure the path is specified correctly.
4. Not specify the option -d and use default database config file under `HOME/.yarr/localdb/HOSTNAME_database.json`.

### Could not parse xxx

**example**

```bash
$ cat database.json
{
    "hostIp": "127.0.0.1",
    "hostPort": "27017",
    "dbName": "localdb",
}
$./bin/dbAccessor -N -d database.json
[  info  ]: DBHandler: Check DB Connection
[  info  ]: ------------------------------
[  info  ]: Function: Initialize upload function and check connection to Local DB
[ error  ]: Could not parse /home/example/YARR/database.json
[ error  ]: 	what(): Expecting property name enclosed in double quotes: line 5 column 1 (char 79)
[  info  ]: ------------------------------


$ cat database.json
{
    "hostIp": "127.0.0.1",
    "hostPort": "27017",
    "dbName": "localdb"
}
$./bin/dbAccessor -N -d database.json
[  info  ]: DBHandler: Check DB Connection
[  info  ]: ------------------------------
[  info  ]: Function: Initialize upload function and check connection to Local DB
[  info  ]: -> Setting database config: /home/kubota/PhD/db/YARR/database.json
[  info  ]: Checking connection to DB Server: mongodb://127.0.0.1:27017/localdb ...
[  info  ]: ---> Good connection!
[  info  ]: ------------------------------
```

**problem**

The [dbAccessor](accessor.md) cannot read the file because of JSON parsing error.

**solution**

Correct the texts of the file according to the error messages said in what().


