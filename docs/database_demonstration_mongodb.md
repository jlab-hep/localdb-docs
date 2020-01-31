# MongoDB

## Getting Start
## Create accounts in mongoDB

```bash
$ cd ~/work/localdb-tools/setting
$ ./create_admin.sh
Authentication succeeded!
Local DB Server IP address: 127.0.0.1
Local DB Server port: 27017
 
Are you sure that's correct? [y/n]
> y

Register localDB admin's username: USERNAME
Register localDB admin's password: 
Successfully added user:
...
For checking the setting of Local DB: /etc/mongod.conf
```

## Lock mongoDB
Change /etc/mongod.conf as bellow:
```bash
$ cat /etc/mongod.conf
# mongod.conf
...
<Documents...>
...
security:
  authorization: "enabled"
...
<Documents...>
...
#snmp:
```
```bash
$ systemctl restart mongod.service
```
Finish installation. Back to the previous page and go to next step.
