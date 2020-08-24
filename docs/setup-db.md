# setup_db.sh

This is a script for setting the configuration of Local DB and checking functions to handle Local DB.

- Location: **YARR/localdb/setup_db.sh**
- Syntax:

```bash
$ cd YARR
$ ./localdb/setup_db.sh [-i address]
                        [-p port]
                        [-n name]
```

### Flow

1. Check the [required packages](requirements-list.md)
2. Check the database config file
    - Create `HOME/.yarr/localdb/HOSTNAME_database.json` if not exist
3. Check the user config file
    - Create `HOME/.yarr/localdb/user.json` if not exist
4. Check the site config file
    - Create `HOME/.yarr/localdb/HOSTNAME_site.json` if not exist
5. Check the command
6. Check the DB connection

### Usage (First Time)

```bash
./setup_db.sh
[LDB]
[LDB] Checking Python Packages ...
[LDB]     ... OK!
[LDB]
[LDB] Checking Database Config
[LDB] -----------------------
[LDB] --  Mongo DB Server  --
[LDB] -----------------------
[LDB] IP address       : 127.0.0.1
[LDB] port             : 27017
[LDB] database name    : localdb
[LDB] -----------------------
[LDB] Are you sure that is correct? (Move to edit mode when answer 'n') [y/n/exit]
[LDB] > y
[LDB] Created Database Config
[LDB]
[LDB] Checking User Config
[LDB] -----------------------
[LDB] --  User Information --
[LDB] -----------------------
[LDB] User Name        : username
[LDB] User Institution : hostname
[LDB] -----------------------
[LDB] Are you sure that is correct? (Move to edit mode when answer 'n') [y/n/exit]
[LDB] > y
[LDB] Created User Config
[LDB]
[LDB] Checking Site Config
[LDB] -----------------------
[LDB] --  Site Information --
[LDB] -----------------------
[LDB] site name        : hostname
[LDB] -----------------------
[LDB] Are you sure that is correct? (Move to edit mode when answer 'n') [y/n/exit]
[LDB] > y
[LDB] Created Site Config
[LDB]
[LDB] Checking the connection...
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017/localdb
#DB INFO# ---> Connection is GOOD.
#DB INFO# -----------------------
[LDB] Done.
```

### Usage (Second Time)

```bash
$./setup_db.sh
[LDB]
[LDB] Checking Python Packages ...
[LDB]     ... OK!
[LDB]
[LDB] Checking Database Config
[LDB WARNING] FOUND DATABASE CONFIG FILE
[LDB] -----------------------
[LDB] --  Mongo DB Server  --
[LDB] -----------------------
[LDB] IP address       : 127.0.0.1 (current 127.0.0.1)
[LDB] port             : 27017     (current 27017)
[LDB] database name    : localdb   (current localdb)
[LDB] -----------------------
[LDB] Are you sure that is correct? (Move to edit mode when answer 'n') [y/n/exit]
[LDB] > y
[LDB] Created Database Config
[LDB]
[LDB] Checking User Config
[LDB WARNING] FOUND USER CONFIG FILE
[LDB] -----------------------
[LDB] --  User Information --
[LDB] -----------------------
[LDB] User Name        : Arisa Kubota
[LDB] User Institution : Tokyo Institute of Technology
[LDB] -----------------------
[LDB] Are you sure that is correct? (Move to edit mode when answer 'n') [y/n/exit]
[LDB] > y
[LDB] Created User Config
[LDB]
[LDB] Checking Site Config
[LDB WARNING] FOUND SITE CONFIG FILE
[LDB] -----------------------
[LDB] --  Site Information --
[LDB] -----------------------
[LDB] site name        : Tokyo Institute of Technology
[LDB] -----------------------
[LDB] Are you sure that is correct? (Move to edit mode when answer 'n') [y/n/exit]
[LDB] > y
[LDB] Created Site Config
[LDB]
[LDB] Checking the connection...
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017/localdb
#DB INFO# ---> Connection is GOOD.
#DB INFO# -----------------------
[LDB] Done.
```

### Additional options

```bash
./setup_db.sh -h

Make some config files and Set some tools for Local DB in HOME/.yarr/localdb by:

    ./setup_db.sh

You can specify the IP address, port number, and DB name of Local DB as following:

    ./setup_db.sh [-i ip address] [-p port] [-n db name]

    - h               Show this usage
    - i <ip address>  Local DB server ip address (default: 127.0.0.1)
    - p <port>        Local DB server port (default: 27017)
    - n <db name>     Local DB Name (default: localdb)
    - r               Clean the settings (reset)
```
