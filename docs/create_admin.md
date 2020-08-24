# create_admin.sh

This is a script for creating an administrator account in Local DB for management of DB & Viewer Application.<br>
You can login MongoDB with the admin account and enable admin functions in the viewer application.<br>
See the [admin functions in the viewer](viewer.md) to get more about what you can do.

- Location: `localdb-tools/setting/create_admin.sh`
- Syntax:
```bash
$ cd localdb-tools/setting
$ ./create_admin.sh [-i address]
                    [-p port]
                    [-a name]
```

### Flow

1. Check the configuration of Local DB server
2. Create system user account in MongoDB of Local DB
    - Provide username
    - Provide password

### Usage

```bash
$ ./create_admin.sh
Authentication succeeded!
Local DB Server IP address: 127.0.0.1
Local DB Server port: 27017

Are you sure thats correct? [y/n]
> y
...
```

This script first displays the configuration of Local DB server.<br>
You need to check it and answer **y** to proceed, or **n** to exit.

```bash
...
Register localDB admins username: username
Register localDB admins password: password
...
```

You can register an administrator account with username and password as follows:

```json
{
    user: username
    roles: [
        "localdb": "userAdmin",
        "localdbtools": "userAdmin",
        "localdb": "readWrite",
        "localdbtools": "readWrite"
    ]
}
```

```bash
...
Successfully added user:

Finished the setting of localdb with certification!!

For checking the setting of Local DB: /etc/mongod.conf
```

This script just creates the account, not change the setting of MongoDB.<br>
If you want to lock MongoDB of Local DB, set `security.authorization: enabled` in `/etc/mongod.conf` and restart mongod service.

### Additional options

```bash
$ ./create_admin.sh -h

Usage:
    ./create_admin.sh [-i ip address] [-p port] [-a admin username]

Options:
    - h                 Show this page
    - i <IP address>    Local DB server IP address, default: 127.0.0.1
    - p <port>          Local DB server port, default: 27017
    - a <admin account> Administrator account username if authentication required
```
