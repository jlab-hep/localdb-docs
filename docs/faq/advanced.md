## MongoDB Setting

### Installation for Local DB Server

Reference: [Install MongoDB](https://docs.mongodb.com/manual/installation/)<br>
Local DB Supports mongo DB server Ver. 4.X or more.

#### a) For centOS7

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

#### b) For MacOS

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

## Mongo Shell

You can use the mongo shell to query and update data.<br>
Please check [The mongo shell](https://docs.mongodb.com/manual/mongo/) to achieve more detail.

### Connect to MongoDB server

```bash
$ export PATH=$PATH:<mongodb installation dir>/bin
$ mongo [--host <IP address>] [--port <port number>]
MongoDB shell version v4.0.12
```

### Database List

```bash
$ mongo
> show dbs
admin            0.000GB
config           0.000GB
local            0.000GB
localdb          1.231GB
```

### Collection List

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

### Document List

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

### Query Document

```bash
> db.component.find({ "_id": ObjectId("5d66e6c54bb3d07690067816") }).pretty()
{
	"_id" : ObjectId("5d66e6c54bb3d07690067816"),
	"serialNumber" : "0x044A",
}
```

## Remote Connection

Local DB supports two methods to connect remotely:

- SSL/TLS Connection
- SSH Tunnel

### SSL/TLS Connection (Recommended)

See [MongoDB documentation for TLS/SSL](https://docs.mongodb.com/manual/tutorial/configure-ssl/) for more information.

#### a) Requirements for DB Server

1. Open the TCP port (e.g. 27017) used by mongod service

```bash
$ sudo firewall-cmd --zone=public --add-port=27017/tcp --permanent
$ sudo firewall-cmd --reload
```

2. Create x.509 certificate for server

See
[Create CA PEM file](https://docs.mongodb.com/manual/appendix/security/appendixA-openssl-ca/) and
[Create Server Certificates](https://docs.mongodb.com/manual/appendix/security/appendixB-openssl-server/#appendix-server-certificate).

```bash
$ sudo cp path/to/CA/file /etc/ssl/localdb_ca.pem
$ sudo cp path/to/certificate/file /etc/ssl/localdb_cert.pem
```

3. Stop MongoDB

```bash
$ sudo systemctl stop mongod
$ sudo vim /etc/mongod.conf
```

4. Set SSL/TLS mode

4.1 Set SSL mode(For MongoDB version 4.0 and earlier)

```yaml
# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1,"DB SERVER HOSTNAME"
  ssl:
    mode: requireSSL
    PEMKeyFile: /etc/ssl/localdb_cert.pem ### Server Certificate
    CAFile: /etc/ssl/localdb_ca.pem ### CA PEM File
```

4.2 Set TLS mode (For MongoDB version 4.2 and greater)

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

5. Start MongoDB

```bash
$ sudo systemctl restart mongod.service
```

6. Confirmation

```bash
# For MongoDB version 4.0 and earlier
$ mongo --ssl --sslPEMKeyFile /etc/ssl/localdb_cert.pem --sslCAFile /etc/ssl/localdb_ca.pem --sslAllowInvalidHostnames --port 27017
# For MongoDB version 4.2 and greater
$ mongo --tls --tlsCertificateKeyFile /etc/ssl/localdb_cert.pem --tlsCAFile /etc/ssl/localdb_ca.pem --tlsAllowInvalidHostnames --port 27017
```

7. Create x.509 certificate for client

See [Create Client Certificates](https://docs.mongodb.com/manual/appendix/security/appendixC-openssl-client/#appendix-client-certificate).

Send the client certificate and CA file to the client machine.

#### b) Remote Connection from the client machine

1. Receive x.509 certificate for client

2. Confirmation

```bash
# For MongoDB version 4.0 and earlier
$ mongo --ssl --sslPEMKeyFile /etc/ssl/localdb_cert.pem --sslCAFile /etc/ssl/localdb_ca.pem --sslAllowInvalidHostnames --port 27017 --host "DB SERVER HOSTNAME"
# For MongoDB version 4.2 and greater
$ mongo --tls --tlsCertificateKeyFile /etc/ssl/localdb_cert.pem --tlsCAFile /etc/ssl/localdb_ca.pem --tlsAllowInvalidHostnames --port 27017 --host "DB SERVER HOSTNAME"
```

### SSH Tunnel

#### a) Requirements for DB Server

1. Stop MongoDB

```bash
$ sudo systemctl stop mongod
$ sudo vim /etc/mongod.conf
```

2. Set SSL mode (For MongoDB version 4.0 and earlier)

```yaml
# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1,"DB SERVER HOSTNAME"
```

3. Start MongoDB

```bash
$ sudo systemctl restart mongod.service
```

4. Create ssh user for the client

```bash
$ sudo useradd <username>
$ sudo passwd <username>
```

#### b) Remote Connection from the client machine

1. Connect to the DB Server by SSH Tunnel

```bash
$ ssh -L 27018:localhost:27017 "DB SERVER HOSTNAME" -fN
```

2. Confirmation

```bash
$ mongo --port 27018
```


## Access Authorization

in edit.

## Convert DB Structure

0. Make a back-up of current Local DB

See [Archive Tool](../tool/archive.md) to make an archive of Local DB, or just execute the sudo command:

```bash
$ sudo systemctl stop mongod.service
$ date=`date +"%y%m%d"`
$ sudo tar zcvf mongo-${date}.tar.gz /var/lib/mongo
$ sudo systemctl restart mongod.service
```

1. Convert DB

`localdb-tools/scripts/tools/make_convert.py` can convert the structure of DB from old one to new one.<br>
Modify the DB setting in following part of `make_convert.py` if needed:

```python
### Set DBs
url = 'mongodb://127.0.0.1:27017'
client = MongoClient( url )
new_db = 'localdb'          # New Local DB (default. localdb)
copy_db = 'localdb_replica' # Replica of the old Local DB (default. localdb_replica)
old_db  = 'yarrdb'          # Old YARR DB (default. yarrdb)
```

And run it:

```bash
$ cd localDB-tools/scripts/tools
$ python3 make_covert.py
# Continue to convert DB: yarrdb/localdb(old) ---> localdb(latest)? (y/n) > y

# Update database scheme: localdb
	2019-10-15T08:11:01 [Start]
  <some texts>
	# Succeeded in Update

# Convert database scheme: yarrdb -> localdb
	2019-10-15T08:11:01 [Start]
  <some texts>
	# Succeeded in Conversion

# Verify database scheme: localdb
	2019-10-15T08:33:52 [Start]
  <some texts>
	# Succeeded in Verification

  <some texts>
	# Succeeded in All Steps
```

It takes about 30 minutes for 1GB data size to complete the conversion. <br>
You can run `make_conver.py` again to restore the replica of DB and start over.
