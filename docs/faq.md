## FAQ 

### the detail of 'setup_db.sh'

`setup_db.sh` can set Local DB commands and the default configuration files for Local DB.

```bash
$ cd YARR
$ ./localdb/setup_db.sh
[LDB] Check the exist site config...NG!

[LDB] Enter the institution name where this machine is, or 'exit' ... 
> INSTITUTION NAME
```

Additional command line arguements:
    
- **-h** : this, prints all available command line arguments
- **-i  ``<IP address>``** : Set IP address of the Local DB Server (default: 127.0.0.1)
- **-p  ``<port number>``** : Set port number of the Local DB Server (default: 27017)
- **-n  ``<database name>``** : Set the Local DB Server Name (default: 'localdb')
- **-r** : Rseet the all settings for Local DB

### '[LDB] Error checking python modules! Exit!'

You are missing some python modules incuded in the requirements.<br>
Check which python module missing by `python3 check_python_modules.py`

```bash
$ python3 check_python_modules.py 
[LDB] Welcome to Local Database Tools!
[LDB] Check Python version ... 3.6 ... OK!
[LDB] Check python modules: 
<some texts>
	requests...not found
	tzlocal...OK!
```

`<module name>...not found!` suggests that `<module name>` is missing,
so install the module by `$ sudo pip3 install <module name>` or `$ pip3 install --user <module name>`.

### '#DB ERROR# The connection of Local DB mongodb://127.0.0.1:27017 is BAD.'

Connection check by `localdbtool-upload init` is failed by some reasons.

1. Uncompleted the setup of Local DB Server

You can check is as following:

```bash
$ mongo
# i. MongoDB not installed
bash: mongo: command not found

# ii. MongoDB not started
<some texts>
exception: connect failed
```

1. MongoDB not installed

You can setup Local DB Server automatically by the script:

```bash
$ git clone https://github.com/jlab-hep/localDB-tools.git
$ cd localDB-tools/setting
$ sudo ./db_server_install.sh
```

Check [Setup Local DB Server](#setup-local-db-server) for more detail.

2. MongoDB not started

You can start/restart/enable Mongo DB by systemctl (centOS7):

```bash
$ systemctl restart mongod.service
$ systemctl enable mongod.service
```

2. Mistake Local DB Server Information

### 'ModuleNotFoundError: No module named "module"'

It is required to install `YARR/localdb/setting/requirements-pip.txt` to use Local DB Tools.<br>
Check the detail in the page 'administrator page'.

## Config Files Sample

### Scan Log File

**Required information**

- 'startTime' or 'timestamp'

