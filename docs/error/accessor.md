# dbAccessor Error Messages

### Table of Contents

- [Not found xxx (File)](#not-found-xxx-file)
    - [Not found database config](#not-found-database-config)
    - [Not found scanLog.json](#not-found-scanlogjson)
- [Not found xxx (Data)](#not-found-xxx-data)
    - [Not found user data](#not-found-user-data)
    - [Not found site data](#not-found-site-data)
    - [Not found component data](#not-found-component-data)
    - [Not found specified relational test run data](#not-found-specified-relational-test-run-data)
- [Found an empty field](#found-an-empty-field)
- [Coult not parse xxx](#could-not-parse-xxx)

---

## Not found xxx (File)

#### Not found database config

**example**

```bash
$./bin/dbAccessor -N -d database.json
...
[  info  ]: -> Setting database config: /home/example/YARR/database.json
[ error  ]: Not found database config.
[ error  ]: Specify the correct path to database config file under -d option.
```

**problem**

The [dbAccessor](../tool/accessor.md) requires to load the [database config file](../config/database.md) to access Local DB, but cannot find the existence of the file in the specified path.

**solution**

- Make sure the [database config file](../config/database.md) exists at the specified path.
- Not specify the option -d and use default [database config file](../config/database.md) under `HOME/.yarr/localdb/HOSTNAME_database.json`.

#### Not found scanLog.json

**example**

```bash
$./bin/dbAccessor -S ./data/last_scan
...
[  info  ]: Cache Directory: /home/example/YARR/data/006192_std_digitalscan
[ error  ]: Not found scanLog.json in /home/example/YARR/data/006192_std_digitalscan
[ error  ]: Specify the correct path to result directory
```

**problem**

The [dbAccessor](../tool/accessor.md) requires to load the [scan log file](../config/scan-log.md) to upload scan results into Local DB, but cannot find the existence of the file in the specified path/directory.

**solution**

Make sure the specified directory is the scan result directory and the [scan log file](../config/scan-log.md) exists in the directory.

## Not found xxx (Data)

#### Not found user data

**example**

```bash
$./bin/dbAccessor -S ./data/last_scan -Q
...
[  info  ]: -> Setting user config: /home/example/.yarr/localdb/user.json
[  info  ]: Loading user information ...
[ error  ]: Not found user data {'username': 'username'} registered in Local DB.
[ error  ]: Please contact Local DB administrator to create your account on Local DB Viewer.
```

**problem**

The user account signed-up on the viewer application is required to upload QC scan results into Local DB, but the [dbAccessor](../tool/accessor.md) cannot confirm the provided user data registered in Local DB.

**solution**

Make sure you signed-up on the viewer application and have your account, and you provide the username correctly in the "viewerUser" field of the [user config file](../config/user.md).

#### Not found site data

**example**

```bash
$./bin/dbAccessor -S ./data/last_scan -Q
...
[  info  ]: -> Setting site config: /home/example/.yarr/localdb/lazulite_site.json
[  info  ]: Loading site information ...
[ error  ]: Not found site data {'institution': 'institution'} registered in Local DB.
[ error  ]: Please set your institution correctly in
[ error  ]: { "code": "xxx" } or { "institution": "xxx" } in /home/example/.yarr/localdb/localhost_site.json
```

**problem**

The site information retrieved from ITk PD is required to upload QC scan results into Local DB, but the [dbAccessor](../tool/accessor.md) cannot confirm the provided site data registered in Local DB.

**solution**

Make sure the site lists retrieved from ITk PD are registered in Local DB, and you provid the institution name/code correctly in the "institution"/"code" field of the [site config file](../config/site.md).

#### Not found component data

**example**

```bash
$./bin/dbAccessor -S ./data/last_scan -Q
...
[  info  ]: Loading component information ...
[ error  ]: Not found component data { "serialNumber": "rd53a", "componentType": "module" } registered in Local DB.
```

**problem**

The component data retrieved from ITk PD is required to upload QC scan results into Local DB, but the [dbAccessor](../tool/accessor.md) cannot confirm the provided component data registered in Local DB.

**solution**

Make sure the component lists retrieved from ITk PD are registered in Local DB.

#### Not found relational test run data in DB

**example**

```bash
$ ./bin/dbAccessor -E dcs.json -s data//last_scan/scanLog.json
...
[ error  ]: Not found relational test run data in DB
[ error  ]: The scan data may not have been uploaded.
[ error  ]: Please make sure it is uploaded and try to upload DCS data again.
```

**problem**

The [dbAccessor](../tool/accessor.md) requires to confirm that the scan result specified by the [scan log file](../config/scan-log.md) has been uploaded into Local DB, but cannot confirm such a scan data registered in Local DB.

**solution**

Make sure to upload the scan result into Local DB.

## Found an empty field

**example**

```bash
$./bin/dbAccessor -S ./data/last_scan -Q
[  info  ]: DBHandler: Register Scan Data
[13:16:46:841][  info  ][   Local DB    ]: ------------------------------
[  info  ]: Function: Upload scan data from specified directory
[  info  ]: Cache Directory: /home/example/YARR/data/006199_std_digitalscan
[  info  ]: -> Setting user config: /home/example/.yarr/localdb/user.json
[  info  ]: -> Setting site config: /home/example/.yarr/localdb/lazulite_site.json
[ error  ]: Found an empty field in json file.
[ error  ]: 	file: connectivity.module  key: serialNumber
[  info  ]: ------------------------------
```

**problem**

The field required to upload data into Local DB is empty.

**solution**

Fill a value in the field of the file.

## Could not parse xxx

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
[  info  ]: -> Setting database config: /home/example/YARR/database.json
[  info  ]: Checking connection to DB Server: mongodb://127.0.0.1:27017/localdb ...
[  info  ]: ---> Good connection!
[  info  ]: ------------------------------
```

**problem**

The [dbAccessor](../tool/accessor.md) cannot read the file because of JSON parsing error.

**solution**

Correct the texts of the file according to the error messages said in what().


