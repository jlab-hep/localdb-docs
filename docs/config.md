# Config Files Sample

### [Database cfg](database-config.md)

### [User cfg](user-config.md)

### [Site cfg](site-config.md)

### [Connectivity cfg](connectivity-config.md)

### [Chip cfg](chip-config.md)

### [scanLog File](scan-log.md)

### [DCS config](dcs-config.md)

### [Viewer Application Cfg](viewer-config.md)

### Component cfg

- `module` : configures for module (option)
- `chipType` : "FEI4B" or "RD53A"
- `chips.i` : configures for chip
    - `serialNumber` : The serial number of the module/chip
    - `componentType` : The component type (e.g. 'Module', 'Front-end Chip')<br>**Select it from the component list in database config.**
    - `chipId`\* : The number of the chipId, which must be "int"

#### For RD53A SCC

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

#### For FEI4B Quad Module

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

### Synchronization Tool

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

### Archive Tool

- `data_path` : path to MongoDB database (defaul. "/var/lib/mongo")
- `archive_path` : path to put archives (Recommendation: use external HDD/SSD)
- `n_archive` : The number of archives want to keep (It depends on size of your disk storage)

```yml
data_path: /var/lib/mongo
archive_path: /root/archive-mongo-data
n_archives: 2
```
