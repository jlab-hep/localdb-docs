# Config Files Sample

## Database cfg

- hostIp => IP address of the Local DB server (default. "127.0.0.1" or "localhost")
- hostPort => The port number of the Local DB server (default. "27017")
- dbName => The name of the Local DB (default. "localdb")

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

- userName: Your name (e.g. "John Doe")
- institution: The institution name you belong (e.g. "ABC Laboratory")
- description: The description for user account (e.g. "account for testbeam")

```json
{
  "userName": "FIRSTNAME LASTNAME",
  "institution": "INSTITUTION",
  "description": "default"
} 
```

## Site cfg

- site: The name of the production site (institution)

```json
{
    "institution": "SITE"
}
```

## Component cfg

- module.serialNumber: The serial number of the module (option)
- module.componentType: "Module" (option)
- chipType: "FEI4B" or "RD53A"
- chips.i.serialNumber: The serial number of the chip
- chips.i.componentType: "Front-end Chip"
- chips.i.chipId: The number of the chipId, which must be "int" 

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

- stage: The test stage, which should be selected from the stage list written in [database.json](#database-cfg)
- module.serialNumber: The serial number of the module
- chipType: "FEI4B" or "RD53A"
- chips.i.serialNumber: The serial number of the chip
- chips.i.config: The path to chip config file
- chips.i.tx: The TX channel, which must be "int"
- chips.i.rx: The RX channel, which must be "int"

### For RD53A
   
```json
{
    "stage": "Testing",
    "module": {
        "serialNumber": "RD53A-001"
    },
    "chipType" : "RD53A",
    "chips" : [
        {
            "serialNumber": "RD53A-001_chip1",
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

- name/Name: The serial number of the chip 
- chipId/ChipId: The geometrical ID of the chip (chipId)

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

- 'status': enabled/disabled to upload data
- 'key': DCS keyword (key list is written in the database config file `${HOME}/.yarr/localdb/database.json`)
- 'num': DCS data number (the combination of DCS keyword and this number specify the DCS data in data file)
- 'description': The description of the DCS data 
- 'path': The path to DCS data file
- 'mode': The mode of DCS setting (e.g. CV) (option)
- 'setting': DCS setting parameter (option)
- 'chip': The chip name related with DCS data (option: if not specified this field, DCS data is stored associated with all chips tested in the specific scan)
 
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

- the 1st line: DCS keyword `key unixtime <key1> <key2> <key3> ...` 
- the 2nd line: DCS number `num null <num1> <num2> <num3> ...`
- After the 3rd line: datetime and DCS data `datetime unixtime <data1> <data2> <data3> ...` (data value must be the number or "null")

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

## Viewer Application

- mongoDB.host: IP address of the Local DB server (default. "127.0.0.1" or "localhost")
- mongoDB.port: The port number of the Local DB server (default. "27017")
- mongoDB.db: The name of the Local DB (default. "localdb")
- mongoDB.username: username of user account in MongoDB if the user authentication is required
- mongoDB.password: password of user account in MongoDB if the user authentication is required
- mongoDB.KeyFile: username & password info file created by [localdb-tools/setting/create_admin.sh]()
- mongoDB.ssl/tls: ssl/tls CA & certification file if ssl/tls is enabled
- userDB.db: The name of the DB for Viewer Application (default. "localdbtool")
- flask.host: IP address running app.py (default. "127.0.0.1" or "localhost")
- flask.port: The port number running app.py (default. "5000")

```yml
# Configs for web viewer

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
