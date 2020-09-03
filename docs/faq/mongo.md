# Simple Setting/Usage of MongoDB

See the [MongoDB docs](https://docs.mongodb.com/manual/) to get more detail.<br>

### Table of Contents

- [Installation for Local DB Server](#installation)
- [mongo shell](#mongo-shell)
- [SSL/TLS Connection](#ssltls-connection)
- [SSH Tunnel](#ssh-tunnel)
- [Access Control](#access-control)

---

## Installation

See the [MongoDB docs: Installation of MongoDB](https://docs.mongodb.com/manual/installation/) to get more detail.<br>
Local DB supports MongoDB server version 4.2 or more.

#### a) for centOS7

###### 1. Add yum repository `/etc/yum.repos.d/mongodb-org-4.2.repo`

```bash
[mongodb-org-4.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.2/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-4.2.asc
```

###### 2. Install by yum

```bash
$ sudo yum install -y mongodb-org.x86_64
```

###### 3. Directories (default)

- shell command: `/bin/mongo`
- process command: `/bin/mongod`
- config file: `/etc/mongod.conf`
- data directory: `/var/lib/mongo`
- log directory: `/var/log/mongodb`

###### 4. Start MongoDB

```bash
$ sudo service mongod start
```

###### 5. Verify that MongoDB has started successfully

```bash
$ mongo
MongoDB shell version v4.2.11
<some texts>
>
```

#### b) for MacOS

###### 1. Install Homebrew

###### 2. Tap the MongoDB Homebrew Tap

```bash
$ brew tap mongodb/brew
```

###### 3. Install MongoDB

```bash
$ brew install mongodb-community@4.2
```

###### 4. Directories (default)

- shell command: `/usr/local/opt/mongodb-community\@4.2/bin/mongo`
- process command: `/usr/local/opt/mongodb-community\@4.2/bin/mongod`
- config file: `/usr/local/etc/mongod.conf`
- data directory: `/usr/local/var/lib/mongo`
- log directory: `/usr/local/var/log/mongodb`

###### 5. Start MongoDB

```bash
$ brew services start mongodb-community@4.2
```

###### 6. Verify that MongoDB has started successfully

```bash
$ export PATH=$PATH:/usr/local/opt/mongodb-community\@4.2/bin
$ mongo
MongoDB shell version v4.2.11
<some texts>
>
```

## Mongo Shell

You can use the mongo shell, which is an interactive interface to MongoDB, to handle data in Local DB.<br>
See the [MongoDB docs: mongo shell](https://docs.mongodb.com/manual/mongo/) to get more detail.

#### Connect to MongoDB server

```bash
$ export PATH=$PATH:<mongodb installation dir>/bin
$ mongo [--host <IP address>] [--port <port number>]
MongoDB shell version v4.2.12
```

#### Database List

```bash
$ mongo
> show dbs
admin            0.000GB
config           0.000GB
local            0.000GB
localdb          1.231GB
```

#### Collection List

```bash
$ mongo
> use localdb
switched to db localdb
> show collections
childParentRelation
chip
comments
component
componentTestRun
config
environment
fs.chunks
fs.files
institution
testRun
user
```

#### Document List

```bash
$ mongo
> use localdb
switched to db localdb
> db.component.find().pretty()
{
	"_id" : ObjectId("5d66e6c54bb3d07690067816"),
	"serialNumber" : "0x044A",
}
{
	"_id" : ObjectId("5d66e6c54bb3d07690067818"),
	"serialNumber" : "0x0445",
}
Type "it" for more
```

#### Query Document

```bash
> db.component.find({ "_id": ObjectId("5d66e6c54bb3d07690067816") }).pretty()
{
	"_id" : ObjectId("5d66e6c54bb3d07690067816"),
	"serialNumber" : "0x044A",
}
```

## SSL/TLS Connection

under implementation.

## SSH Tunnel

You can use SSH tunnel to access Local DB remotely from an external server.

#### a) Requirements for DB Server

###### 1. Stop MongoDB

```bash
$ sudo systemctl stop mongod
$ sudo vim /etc/mongod.conf
```

###### 2. Set the IP address of the host server

```yaml
# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1,"DB SERVER HOSTNAME" # e.g. 127.0.0.1,192.168.1.50
```

###### 3. Start MongoDB

```bash
$ sudo systemctl restart mongod.service
```

###### 4. Create ssh user for the client

```bash
$ sudo useradd <username>
$ sudo passwd <username>
```

#### b) Remote Connection from the client machine

###### 1. Connect to the DB Server by SSH Tunnel

```bash
$ ssh -L 27018:localhost:27017 username@hostname -fN
```

###### 2. Confirmation

```bash
$ mongo --port 27018
```

## Access Control

You can enable access control on Mongo DB and Local DB features support the authentication mechanisms; SCRAM, x509.<br>
See the [MongoDB docs: Enable Access Control](https://docs.mongodb.com/manual/tutorial/enable-authentication/) to get more detail.<br>

###### 1. Start MongoDB without access control

Stop MongoDB instance:

```bash
$ sudo systemctl stop mongod.service
```

Disable or comment out security.authorization in /etc/mongod.conf:

```yml
...
security:
    authorization: disabled
...
```

Start MongoDB instance:

```bash
$ sudo systemctl start mongod.service
```

###### 2. Create the user administrator

Restart MongoDB and create the user administrator account for MongoDB:

```bash
$ mongo --port 27017
> use admin
> db.createUser({user:"myUserAdmin",pwd:passwordPrompt(),roles:[{role:"userAdminAnyDatabase",db:"admin"},"readWriteAnyDatabase"]})
Enter password: xxxxxxx
Successfully added user: {
	"user" : "myUserAdmin",
	"roles" : [
		{
			"role" : "userAdminAnyDatabase",
			"db" : "admin"
		},
		"readWriteAnyDatabase"
	]
}
> exit
```

###### 3. Create the Local DB administrator

Run [localdb-tools/setting/create_admin.sh](script/create_admin.md) to create the administrator account for Local DB:

```bash
$ cd localdb-tools/setting
$ ./create_admin.sh -p 27017
```

!!! Note
    This Local DB administrator account is mainly used to enable admin functions in the [viewer application](tool/viewer.md), and it has access authority only to the database related to Local DB.<br>
    It is recommended to create this account with a username and password different from the user administrator account created in the previous step to improve the security of DB.

###### 4. Restart MongoDB with access control

Stop MongoDB instance:

```bash
$ sudo systemctl stop mongod.service
```

Enable or uncomment out security.authorization in /etc/mongod.conf:

```yml
...
security:
    authorization: enabled
...
```

Start MongoDB instance:

```bash
$ sudo systemctl start mongod.service
```

###### 5. Connect and authenticate as the user administrator

```bash
$ mongo --port 27017 --authenticationDatabase "admin" -u "myUserAdmin" -p
Enter password: xxxxxxxx
connecting to: ...
> exit
```

###### 6. Connect and authenticate as the Local DB administrator

```bash
$ mongo --port 27017 --authenticationDatabase "localdb" -u "myLocalDbAdmin" -p
Enter password: xxxxxxxx
connecting to: ...
> exit
```
