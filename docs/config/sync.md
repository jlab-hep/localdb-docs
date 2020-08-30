# Synchronization Tool Config

You can specify the configuration of Local DB server and Master Local DB server to sync them.

#### File Format

Sync Tool configuration file uses the YAML format:

```yml
local:
    host: 127.0.0.1
    port: 27017
    #username: username
    #password: ihatepassword
master:
    host: master-host
    port: 27017
    #username: username
    #password: ihatepassword
#logfile: logs/production.log
```

#### Option

##### local Options

```yml
local:
    host: 127.0.0.1
    port: 27017
    #username: username
    #password: ihatepassword
```

Specifies the configuration of the local MongoDB server.

- `local.host`<br>
_Default_ : 127.0.0.1<br>
Specifies IP address of the host machine where MongoDB is running.

- `local.port`<br>
_Default_ : 27017<br>
Specifies the port number where the MongoDB is listhening.

- `local.username`<br>
Specifies username of user account in MongoDB if the user authentication is required.

- `local.password`<br>
Specifies password of user account in MongoDB if the user authentication is required.

##### master Options

```yml
master:
    host: master-host
    port: 27017
    #username: username
    #password: ihatepassword
```

Specifies the configuration of the master MongoDB server.<br>
Please ask to the manager of DB server for `host`, `port`, `username` and `password` of master MongoDB.

##### log Option

- `logfile`<br>
_Default_ : ./log<br>
Specifies path to log output file.


