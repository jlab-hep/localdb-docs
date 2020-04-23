# create_admin.sh

This is a script for setting administrator account in Local DB for management of DB & Viewer Application.<br>
It's located in here: [localdb-tools/setting/create_admin.sh](https://gitlab.cern.ch/YARR/localdb-tools/-/blob/master/setting/create_admin.sh)

### Flow

1. Check the DB server information
2. Set username and password
3. Create administrator account for Local DB

### Usage

```bash
./create_admin.sh
Authentication succeeded!
Local DB Server IP address: 127.0.0.1
Local DB Server port: 27017

Are you sure that's correct? [y/n]
> y

Register localDB admin's username: username
Register localDB admin's password: Successfully added user:
    user: username
    roles: [ 'localdb': 'readWrite', 'localdbtools': 'readWrite' ]


Finished the setting of localdb with certification!!

For checking the setting of Local DB: /etc/mongod.conf
```

### Additional options

```bash
./create_admin.sh -h

Usage:
    ./create_admin.sh [-i ip address] [-p port] [-a admin username]

Options:
    - h                 Show this page
    - i <IP address>    Local DB server IP address, default: 127.0.0.1
    - p <port>          Local DB server port, default: 27017
    - a <admin account> Administrator account username if authentication required
```
