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

1. Check the [required packages](../installation/requirements-list.md)
2. Check the database config file
    - Create `HOME/.yarr/localdb/HOSTNAME_database.json` if not exist
3. Check the user config file
    - Create `HOME/.yarr/localdb/user.json` if not exist
4. Check the site config file
    - Create `HOME/.yarr/localdb/HOSTNAME_site.json` if not exist
5. Check the command
6. Check the DB connection

### Usage

```bash
$ cd YARR/localdb
$ ./setup_db.sh
[LDB] Set editor command ... (e.g. nano, vim, emacs)
[LDB] > vim
```

This script first ask you which editor command to use when editing the file interactively.

```bash
### script output
[LDB] Checking Python Packages ...
[LDB]     ... OK!
```

Next the script checks that the required python packages is installed.<br>
The output of **OK** means that the installation is confirmed.<br>
If some packages are not installed, the script displays error messages:

```bash
### script output
[LDB] Checking Python Packages ...
[LDB ERROR] There are missing pip modules:
[LDB ERROR] - arguments
[LDB ERROR]
[LDB ERROR] Install them by:
[LDB ERROR] python3 -m pip install --user -r ./setting/requirements-pip.txt
```

At that time, install the packages written in **YARR/localdb/setting/requirements-pip.txt**:

```bash
$ python3 -m pip install --user -r ./setting/requirements-pip.txt
```

Once installed, run **setup_db.sh** again.

```bash
### script output
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
```

The script next checks the configuration of running MongoDB to set Local DB.<br>
Answer **y** to proceed if you did not change any settings when you installed MongoDB.<br>
If you have changed any value, answer **n** and move to edit mode and change the configuration appropriately.<br>
The script creates the [database config file](../config/database.md) at **HOME/.yarr/localdb/HOSTNAME_database.json**.

```bash
### script output
[LDB] Checking User Config
[LDB] -----------------------
[LDB] --  User Information --
[LDB] -----------------------
[LDB] User Name        : username
[LDB] User Institution : hostname
[LDB] -----------------------
[LDB] Are you sure that is correct? (Move to edit mode when answer 'n') [y/n/exit]
[LDB] > y
```

The script next checks the configuration of user.<br>
Answer **n** and change the user config file to your name and institution name.<br>
The script creates the [user config file](../config/user.md) at **HOME/.yarr/localdb/user.json**.

```bash
### script output
[LDB] Checking Site Config
[LDB] -----------------------
[LDB] --  Site Information --
[LDB] -----------------------
[LDB] site name        : hostname
[LDB] -----------------------
[LDB] Are you sure that is correct? (Move to edit mode when answer 'n') [y/n/exit]
[LDB] > y
```

The script next checks the configuration of site.<br>
Answer **n** and change the site name to your institution name or where you are.<br>
The script creates the [site config file](../config/site.md) at **HOME/.yarr/localdb/HOSTNAME_site.json**.


```bash
### script output
[LDB] Checking the connection...
[  info  ]: ------------------------------
[  info  ]: Function: Initialize upload function and check connection to Local DB
[  info  ]: -> Setting database config: /home/.yarr/localdb/localhost_database.json (default)
[  info  ]: Checking connection to DB Server: mongodb://127.0.0.1:27000/localdb ...
[  info  ]: ---> Good connection!
[  info  ]: ------------------------------
[LDB] Done.
```

Finally the script checks the connection to Local DB.<br>
The output of "Good connection!" means that the connection can be confirmed.<br>
If the connection cannot be established, the script displayes error messages:

```bash
### script output
[LDB] Checking the connection...
[  info  ]: ------------------------------
[  info  ]: Function: Initialize upload function and check connection to Local DB
[  info  ]: -> Setting database config: /home/.yarr/localdb/localhost_database.json (default)
[  info  ]: Checking connection to DB Server: mongodb://127.0.0.1:27000/localdb ...
[ error  ]: ---> Bad connection.
[ error  ]:      127.0.0.1:27017: [Errno 111] Connection refused
[  info  ]: ------------------------------
```

See the [solution in the bad connection](../faq.md) in this case.

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
