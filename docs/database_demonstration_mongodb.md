# MongoDB

## Create accounts in mongoDB
Create an account in mongoDB with bellow commands.<br>
Input username and password as you like.(e.g.: USERNAME=hokuyama, PASSWORD=itkweek)<br>
<span style="color: red; ">**These are used as LocalDB admin's username and password from here.**</span>

```bash
$ cd ~/work/localdb-tools/setting
$ ./create_admin.sh
Authentication succeeded!
Local DB Server IP address: 127.0.0.1
Local DB Server port: 27017
 
Are you sure thats correct? [y/n]
> y

Register localDB admins username: USERNAME
Register localDB admins password: 
Successfully added user:
...
For checking the setting of Local DB: /etc/mongod.conf
```

## Lock mongoDB
Lock the mongoDB so that only those who know the account name and password can see and write to it.<br>
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
Reload config file and restart mongoDB with the bellow command.
```bash
$ systemctl restart mongod.service
```
Finish mongoDB setting. Back to the previous page and go to next step.
