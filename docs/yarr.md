## About

### 3. scanConsole with Local DB

#### Check Registered Component Data

You can check all component data registered in Local DB Server by `localdbtool-upload check`

```bash
$ ./localdb/bin/localdbtool-upload check comp
```

#### Check Chip Data

You can check all chip data tested by `localdbtool-upload check`

```bash
$ ./localdb/bin/localdbtool-upload check chip
```

## Quick Installation 

### Installation for Local DB Server

Reference: [Install MongoDB](https://docs.mongodb.com/manual/installation/)<br>
Local DB Supports mongo DB server Ver. 4.X or more.

- For centOS7

1. Add yum repository `/etc/yum.repos.d/mongodb-org-4.2.repo`

```bash
[mongodb-org-4.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.2/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-4.2.asc
```

2. Install by yum

```bash
$ sudo yum install -y mongodb-org.x86_64
```

3. Directories (default)

- shell command: `/bin/mongo`
- process command: `/bin/mongod`
- config file: `/etc/mongod.conf`
- data directory: `/var/lib/mongo`
- log directory: `/var/log/mongodb`

4. Start MongoDB

```bash
$ sudo service mongod start
```

5. Verify that MongoDB has started successfully

```bash
$ mongo
MongoDB shell version v4.0.11
<some texts>
> 
```

If you want to enable access authorization, check [Access Authorization](#access-authorization)

- For MacOS

1. Install Homebrew

2. Tap the MongoDB Homebrew Tap

```bash
$ brew tap mongodb/brew
```

3. Install MongoDB

```bash
$ brew install mongodb-community@4.0
```

4. Directories (default)

- shell command: `/usr/local/opt/mongodb-community\@4.0/bin/mongo`
- process command: `/usr/local/opt/mongodb-community\@4.0/bin/mongod`
- config file: `/usr/local/etc/mongod.conf`
- data directory: `/usr/local/var/lib/mongo`
- log directory: `/usr/local/var/log/mongodb`

5. Start MongoDB

```bash
$ brew services start mongodb-community@4.0
```

6. Verify that MongoDB has started successfully

```bash
$ export PATH=$PATH:/usr/local/opt/mongodb-community\@4.0/bin
$ mongo
MongoDB shell version v4.0.11
<some texts>
> 
```

### Installation of Local DB Tools

[Local DB Tools repository](https://github.com/jlab-hep/localDB-tools)

```bash
$ git clone https://github.com/jlab-hep/localDB-tools.git
$ cd localDB-tools/setting
$ sudo pip3 install -r requirements-pip.txt
```

#### Viewer Application

Web Application which can check data stored in Local DB.

```bash
$ cd localDB-tools/viewer
$ ./setup_viewer.sh
$ python3 app.py --config conf.yml &
```

Check `http://localhost:5000/localdb/` in local browser.<br>
If you want to check data remotely, check [here](#remote-connection)

#### Synchronization Tool

Command which can synchroniza data between other Local DB Server.

## Remote Connection

Local DB supports two methods to connect remotely:

- SSL/TLS Connection
- SSH Tunnel

### SSL/TLS Connection (Recommended)

See [MongoDB documentation for TLS/SSL](https://docs.mongodb.com/manual/tutorial/configure-ssl/) for more information.

#### Requirements for DB Server

- Open the TCP port (e.g. 27017) used by mongod service 

```bash
$ sudo firewall-cmd --zone=public --add-port=27017/tcp --permanent
$ sudo firewall-cmd --reload
```

- Create x.509 certificate for server

See 
[Create CA PEM file](https://docs.mongodb.com/manual/appendix/security/appendixA-openssl-ca/) and 
[Create Server Certificates](https://docs.mongodb.com/manual/appendix/security/appendixB-openssl-server/#appendix-server-certificate).

```bash
$ sudo cp path/to/CA/file /etc/ssl/localdb_ca.pem
$ sudo cp path/to/certificate/file /etc/ssl/localdb_cert.pem
```

- Stop MongoDB

```bash
$ sudo systemctl stop mongod
$ sudo vim /etc/mongod.conf
```

- Set SSL mode (For MongoDB version 4.0 and earlier)

```yaml
# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1, "DB SERVER HOSTNAME"
  ssl:
    mode: requireSSL
    PEMKeyFile: /etc/ssl/localdb_cert.pem ### Server Certificate
    CAFile: /etc/ssl/localdb_ca.pem ### CA PEM File
```

- Set TLS mode (For MongoDB version 4.2 and greater)

```yaml
# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1, "DB SERVER HOSTNAME"
  tls:
    mode: requireTLS
    certificateKeyFile: /etc/ssl/localdb_cert.pem ### Server Certificate
    CAFile: /etc/ssl/localdb_ca.pem ### CA PEM File
```

- Start MongoDB

```bash
$ sudo systemctl restart mongod.service
```

- Confirmation

```bash
# For MongoDB version 4.0 and earlier
$ mongo --ssl --sslPEMKeyFile /etc/ssl/localdb_cert.pem --sslCAFile /etc/ssl/localdb_ca.pem --sslAllowInvalidHostnames --port 27017
# For MongoDB version 4.2 and greater
$ mongo --tls --tlsCertificateKeyFile /etc/ssl/localdb_cert.pem --tlsCAFile /etc/ssl/localdb_ca.pem --tlsAllowInvalidHostnames --port 27017
```

- Create x.509 certificate for client 

See [Create Client Certificates](https://docs.mongodb.com/manual/appendix/security/appendixC-openssl-client/#appendix-client-certificate).

Send the client certificate and CA file to the client machine.

#### Remote Connection from the client machine

- Receive x.509 certificate for client 

- Confirmation

```bash
# For MongoDB version 4.0 and earlier
$ mongo --ssl --sslPEMKeyFile /etc/ssl/localdb_cert.pem --sslCAFile /etc/ssl/localdb_ca.pem --sslAllowInvalidHostnames --port 27017 --host "DB SERVER HOSTNAME"
# For MongoDB version 4.2 and greater
$ mongo --tls --tlsCertificateKeyFile /etc/ssl/localdb_cert.pem --tlsCAFile /etc/ssl/localdb_ca.pem --tlsAllowInvalidHostnames --port 27017 --host "DB SERVER HOSTNAME"
```

### SSH Tunnel

#### Requirements for DB Server

- Stop MongoDB

```bash
$ sudo systemctl stop mongod
$ sudo vim /etc/mongod.conf
```

- Set SSL mode (For MongoDB version 4.0 and earlier)

```yaml
# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1, "DB SERVER HOSTNAME"
```

- Start MongoDB

```bash
$ sudo systemctl restart mongod.service
```

- Create ssh user for the client

```bash
$ sudo useradd <username>
$ sudo passwd <username>
```

#### Remote Connection from the client machine

- Connect to the DB Server by SSH Tunnel

```bash
$ ssh -L 27018:localhost:27017 "DB SERVER HOSTNAME" -fN
```

- Confirmation

```bash
$ mongo --port 27018 
```

## Access Authorization

in edit


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

## Database Structure

![Database Structure](images/localdb_structure.png)
