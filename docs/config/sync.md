### Synchronization Tool

- `local` : configures for local MongoDB server
    - `host` : IP address of MongoDB (default. "127.0.0.1" or "localhost")
    - `port` : The port number of MongoDB (default. "27017")
    - `username` : username of user account in MongoDB if the user authentication is required
    - `password` : password of user account in MongoDB if the user authentication is required
- `master` : configures for master MongoDB server <br>
    Please ask to the manager of DB server for `host`, `port`, `username` and `password` of master MongoDB
- `logfile` : path to log output file

```yml
local:
    host: 127.0.0.1
    port: 27017
    #username: tokyotech
    #password: ihatepassword
master:
    host: master-host
    port: 27017
    #username: tokyotech
    #password: ihatepassword
#logfile: logs/production.log
```


