# Config Files Sample

**key with \* is a required content**

## Database cfg

- `hostIp` : IP address of the Local DB server (default. "127.0.0.1" or "localhost")
- `hostPort` : The port number of the Local DB server (default. "27017")
- `dbName` : The name of the Local DB (default. "localdb")

```json
{
    "hostIp": "127.0.0.1",
    "hostPort": "27017",
    "dbName": "localdb",
    "ssl": {
        "enabled": false,
        "PEMKeyFile": null,
        "CAFile": null
    },
    "tls": {
        "enabled": false,
        "CertificateKeyFile": null,
        "CAFile": null
    },
    "auth": "default",
    "KeyFile": null,
    "verify": false,
    "stage": [
        "Bare Module",
        "Wire Bonded",
        "Potted",
        "Final Electrical",
        "Complete",
        "Loaded",
        "Parylene",
        "Initial Electrical",
        "Thermal Cycling",
        "Flex + Bare Module Attachment",
        "Testing"
    ],
    "environment": [
        "vddd_voltage",
        "vddd_current",
        "vdda_voltage",
        "vdda_current",
        "hv_voltage",
        "hv_current",
        "temperature"
    ],
    "component": [
        "Front-end Chip",
        "Front-end Chips Wafer",
        "Hybrid",
        "Module",
        "Sensor Tile",
        "Sensor Wafer"
    ]
}
```

## User cfg

- `userName` : Your name (e.g. "John Doe")
- `institution` : The institution name you belong (e.g. "ABC Laboratory")
- `description` : The description for user account (e.g. "account for testbeam")

```json
{
  "userName": "FIRSTNAME LASTNAME",
  "institution": "INSTITUTION",
  "description": "default"
}
```

## Site cfg

- `site` : The name of the production site (institution)

```json
{
    "institution": "SITE"
}
```

## Component cfg

- `module` : configures for module (option)
- `chipType` : "FEI4B" or "RD53A"
- `chips.i` : configures for chip
    - `serialNumber` : The serial number of the module/chip
    - `componentType` : The component type (e.g. 'Module', 'Front-end Chip')<br>**Select it from the component list in database config.**
    - `chipId`\* : The number of the chipId, which must be "int"

### For RD53A SCC

```json
{
    "chipType" : "RD53A",
    "chips" : [
        {
            "serialNumber": "RD53A-001",
            "componentType": "Front-end Chip",
            "chipId": 0
        }
    ]
}
```

### For FEI4B Quad Module

```json
{
    "module": {
        "serialNumber": "FEI4B-001",
        "componentType": "Module"
    },
    "chipType" : "FEI4B",
    "chips" : [
        {
            "serialNumber": "FEI4B-001-001",
            "componentType": "Front-end Chip",
            "chipId": 1
        },
        {
            "serialNumber": "FEI4B-001-002",
            "componentType": "Front-end Chip",
            "chipId": 2
        },
        {
            "serialNumber": "FEI4B-001-003",
            "componentType": "Front-end Chip",
            "chipId": 3
        },
        {
            "serialNumber": "FEI4B-001-004",
            "componentType": "Front-end Chip",
            "chipId": 4
        }
    ]
}
```

## Connectivity cfg

- `stage` : The test stage, which should be selected from the stage list written in [database.json](#database-cfg)
- `module` : configures for module (option)<br>**Must be set when uploading the test data in association with the MODULE.**
- `chipType` : "FEI4B" or "RD53A"
- `chips.i` : configures for chip
    - `serialNumber` : The serial number of the module/chip.<br>**Ensure the same as 'Name' written in chip config file.**
    - `config` : The path to chip config file (only in `chip.i`)
    - `tx` : The TX channel, which must be "int" (only in `chip.i`)
    - `rx` : The RX channel, which must be "int" (only in `chip.i`)

### For RD53A

```json
{
    "stage": "Testing",
    "chipType" : "RD53A",
    "chips" : [
        {
            "serialNumber": "RD53A-001",
            "config" : "configs/chip1.json",
            "tx" : 0,
            "rx" : 0
        }
    ]
}
```
### For FEI4B

```json
{
    "stage": "Testing",
    "module": {
        "serialNumber": "FEI4B-001"
    },
    "chipType" : "FEI4B",
    "chips" : [
        {
            "serialNumber": "FEI4B-001-chip1",
            "config" : "configs/chip1.json",
            "tx" : 0,
            "rx" : 0
        },
        {
            "serialNumber": "FEI4B-001-chip2",
            "config" : "configs/chip2.json",
            "tx" : 0,
            "rx" : 1
        },
        {
            "serialNumber": "FEI4B-001-chip3",
            "config" : "configs/chip3.json",
            "tx" : 0,
            "rx" : 2
        },
        {
            "serialNumber": "FEI4B-001-chip4",
            "config" : "configs/chip4.json",
            "tx" : 0,
            "rx" : 3
        }
    ]
}
```

## Chip cfg

You can replicated it from `YARR/configs/defaults/<FE>.json`.

- `name`/`Name` : The serial number of the chip
- `chipId`/`ChipId` : The geometrical ID of the chip (chipId)

### For RD53A

```json
{
    "RD53A": {
        "Parameter": {
            "ChipId": 0,
            "Name": "RD53A-001"
        }
    }
}
```

### For FEI4B

```json
{
    "FE-I4B": {
        "Parameter": {
            "chipId": 0
        },
        "name": "FEI4B-001-001"
    }
}
```

## DCS cfg

- `status` : enabled/disabled to upload data
- `key` : DCS keyword (key list is written in the database config file `${HOME}/.yarr/localdb/database.json`)
- `num` : DCS data number (the combination of DCS keyword and this number specify the DCS data in data file)
- `description` : The description of the DCS data
- `path` : The path to DCS data file
- `mode` : The mode of DCS setting (e.g. CV) (option)
- `setting` : DCS setting parameter (option)
- `chip` : The chip name related with DCS data (option) <br>**If not specified this field, DCS data is stored associated with all chips tested in the specific scan.**

```json
{
    "environments": [{
        "description": "VDDD Voltage [V]",
        "key": "vddd_voltage",
        "num": 0,
        "path": "dcs.dat",
        "status": "disabled"
    },{
        "description": "VDDD Current [A]",
        "key": "vddd_current",
        "num": 0,
        "path": "dcs.dat",
        "status": "disabled"
    },{
        "description": "VDDA Voltage [V]",
        "key": "vdda_voltage",
        "num": 0,
        "path": "dcs.dat",
        "status": "disabled"
    },{
        "description": "VDDA Current [A]",
        "key": "vdda_current",
        "num": 0,
        "path": "dcs.dat",
        "status": "disabled"
    },{
        "description": "High Voltage [V]",
        "key": "hv_voltage",
        "num": 0,
        "path": "dcs.dat",
        "status": "disabled"
    },{
        "description": "High Voltage Current [A]",
        "key": "hv_current",
        "num": 0,
        "path": "dcs.dat",
        "status": "disabled"
    },{
        "description": "Chip Temperature [C]",
        "key": "temperature",
        "num": 0,
        "path": "dcs.dat",
        "chip": "JohnDoe_0",
        "status": "disabled"
    },{
        "description": "Module Temperature [C]",
        "key": "temperature",
        "num": 1,
        "path": "dcs.dat",
        "status": "disabled"
    }]
}
```

## DCS Data File

- the 1st line : DCS keyword `key unixtime <key1> <key2> <key3> ...`
- the 2nd line : DCS number `num null <num1> <num2> <num3> ...`
- After the 3rd line : datetime and DCS data `datetime unixtime <data1> <data2> <data3> ...` (data value must be the number or "null")

```dat
key unixtime vddd_voltage vddd_current vdda_voltage vdda_current
num null 0 0 0 0
2019-06-24_20:49:13 1561376953 10 20 0 0
2019-06-24_20:49:23 1561376963 11 21 0 0
2019-06-24_20:49:33 1561376973 12 22 0 0
2019-06-24_20:49:43 1561376983 13 23 0 0
2019-06-24_20:49:53 1561376993 14 24 0 0
2019-06-24_20:50:03 1561377003 15 25 0 0
```

## scanLog File

- `startTime`\* / `timestamp`\*: timestamp of the test (unixtime (startTime) or string (timestamp))

```json
{
    "startTime": 1569924977,
    "timestamp": "2019-10-01_19:16:17"
}
```

## Viewer Application

- `mongoDB` : configures for Local DB (MongoDB) server
    - `host` : IP address of DB server (default. "127.0.0.1" or "localhost")
    - `port` : The port number of DB server (default. "27017")
    - `db` : The name of DB (default. "localdb")
    - `username` : username of user account in MongoDB if the user authentication is required
    - `password` : password of user account in MongoDB if the user authentication is required
    - `KeyFile` : username & password info file created by [localdb-tools/setting/create_admin.sh]()
    - `ssl/tls` : ssl/tls CA & certification file if ssl/tls is enabled
- `userDB` : configures for Local User DB which is DB for localdb-tools
    - `db` : The name of DB (default. "localdbtool")
- `flask` : configures for flask server
    - `host` : IP address of flask server (default. "127.0.0.1" or "localhost")<br>**Set host IP address if access remotely.**
    - `port` : The port number of flask server (default. "5000")<br>**Open firewall port if access remotely.**

```yml
mongoDB:
    host: 127.0.0.1 # IP address running mongoDB
    port: 27017     # port number running mongoDB
    db: localdb     # local database name
    username: # username of user account in MongoDB
    password: # password of user account in MongoDB
    KeyFile: #localdbkeypass # path/to/user/key/file
    ssl:
        enabled: False
        CAFile: # path/to/CA/file
        PEMKeyFile: # path/to/certificate/file
    tls:
        enabled: False
        CAFile: # path/to/CA/file
        CertificateFile: # path/to/certificate/file
userDB:
    db: localdbtools
flask:
    host: 127.0.0.1 # IP address running app.py
    port: 5000      # port number running app.py
# For development
#is_development: True
```

## Synchronization Tool

- `local` : configures for local MongoDB server
    - `host` : IP address of MongoDB (default. "127.0.0.1" or "localhost")
    - `port` : The port number of MongoDB (default. "27017")
    - `username` : username of user account in MongoDB if the user authentication is required
    - `password` : password of user account in MongoDB if the user authentication is required
- `master` : configures for master MongoDB server <br>
    Please ask to the manager of DB server for `host`, `port`, `username` and `password` of master MongoDB
- `logfile` : path to log output file

```yml
local:
    host: 127.0.0.1
    port: 27017
    #username: tokyotech
    #password: ihatepassword
master:
    host: master-host
    port: 27017
    #username: tokyotech
    #password: ihatepassword
#logfile: logs/production.log
```

## Archive Tool

- `data_path` : path to MongoDB database (defaul. "/var/lib/mongo")
- `archive_path` : path to put archives (Recommendation: use external HDD/SSD)
- `n_archive` : The number of archives want to keep (It depends on size of your disk storage)

```yml
data_path: /var/lib/mongo
archive_path: /root/archive-mongo-data
n_archives: 2
```
