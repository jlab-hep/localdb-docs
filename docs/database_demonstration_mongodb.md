# MongoDB

## Getting Start

Just type 'mongo' to check if the MongoDB service is running.

```bash
$ mongo
MongoDB shell version v3.6.16
> exit
bye
$
```

<!--
If the service doesn't seem to be running,<br>
maybe the package has not been installed or the service has not been started, <br>
so please check [pre requirement page](requirements.md) to install/start the service.
-->

Finish!

## Create accounts in mongoDB

```bash
$ cd localdb-tools/setting
$ ./create_admin.sh
...
```

## Lock mongoDB and add bindIp
Change /etc/mongod.conf as bellow:
```bash
$ cat /etc/mongod.conf
# mongod.conf

# for documentation of all options, see:
#   http://docs.mongodb.org/manual/reference/configuration-options/

# where to write logging data.
systemLog:
  destination: file
  logAppend: true
  path: /var/log/mongodb/mongod.log

# Where and how to store data.
storage:
  dbPath: /var/lib/mongo
  journal:
    enabled: true
#  engine:
#  wiredTiger:

# how the process runs
processManagement:
  fork: true  # fork and run in background
  pidFilePath: /var/run/mongodb/mongod.pid  # location of pidfile
  timeZoneInfo: /usr/share/zoneinfo

# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1,{IP of DB machine}  # Enter 0.0.0.0,:: to bind to all IPv4 and IPv6 addresses or, alternatively, use the net.bindIpAll setting.

security:
  authorization: "enabled"
...
```
```bash
$ systemctl restart mongod.service
```


## Open port
```bash
$ firewall-cmd --zone=public --add-port=27017/tcp --permanent
$ firewall-cmd --reload
$ firewall-cmd --list-all
```

