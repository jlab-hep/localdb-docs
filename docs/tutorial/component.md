# Component Tutorial

This tutorial describes the operations related to the component registration.

!!! Note
    Local DB supports the component data registered in ITk PD for QC.<br>
    But if you want to register the component data other than QC components, you can register the component data directly into Local DB.

### Table of Contents

1. [How to Register Component Data in ITk PD](#1-how-to-register-component-in-itk-pd)
2. [How to Retrieve Component Data from ITk PD into Local DB](#2-how-to-retrieve-component-from-itk-pd)
3. [How to Register Component Data Directly into Local DB](#3-how-to-register-component-in-local-db)

---

## 1. How to Register Component in ITk PD

in edit.


## 2. How to Register Component in Local DB

First make sure to prepare the [user config file](../config/user.md) and the [site config file](../config/site.md) by [YARR/localdb/setup_db.sh](../script/setup-db.md):

```bash
$ cd YARR
$ ./localdb/setup_db.sh -p 27017
```

Next prepare the [component config file (component.json)](../config/component.md):

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


Then you can register component data into Local DB by [YARR/bin/dbAccessor](../tool/accessor.md):

```bash
$ ./bin/dbAccessor -C -c component.json -u $HOME/.yarr/localdb/user.json -i $HOME/.yarr/localdb/$HOSTNAME_site.json

<lots of text>
[warning ]: It will be override with the provided infomation if data already exists in Local DB.
[warning ]: Do you continue to upload data into Local DB? [y/n]
[warning ]: (Please answer Y/y to continue or N/n to exit.)
[y/n]: y
```

Answer **y** to proceed or **n** to exit.

```bash
### script output
[  info  ]: Succeeded uploading component data
```

The output of "Succeeded uploading" means that data was uploaded into Local DB successfully.<br>
You can retrieve/create [connectivity config file](../config/connectivity.md) according to the component data by [YARR/bin/dbAccessor](../tool/accessor.md):

```bash
$ ./bin/dbAccessor -D -n RD53A-001
```

You can upload scan result associated with the registered component data using the [connectivity config](../config/connectivity.md):

```bash
$ ./bin/scanConsole \
-c db-data/connectivity.json \
-r configs/controller/emuCfg_rd53a.json \
-s configs/scans/rd53a/std_digitalscan.json \
-W
<lots of text>
[  info  ]: Succeeded uploading component data
```

The output of "Succeeded uploading" means that data was uploaded into Local DB successfully.<br>
