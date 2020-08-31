# Common Error Messages

### Table of Contents

- [Missing PIP Modules](#missing-pip-modules)
- [Local DB Connection Refused](#local-db-connection-refused)

---

## Missing PIP Modules

If there is some missing pip modules in the setup script, an error will be output and the process will be terminated.<br>
You can install pip modules by:

```bash
$ sudo python3 -m pip install <module>
```

You can also install them locally if you do not have root privileges by:

```bash
$ python3 -m pip install --user <module>
```

## Local DB Connection Refused

If the connection check to Local DB fails in some tools, an error will be output:

```bash
[ error ] 127.0.0.1:27017: [Errno 111] Connection refused
```

In this case, MongoDB instance may not be started with the specified IP address and port number.<br>
Check it by:

```bash
$ mongo --host 127.0.0.1 --port 27017
```

##### a. Start normally

```bash
MongoDB shell version v4.2.6
connecting to: mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb
---
>
```

If it starts normally, the IP address or port nomber specified in the [configuration file](../config.md) of the tool is incorrect.

##### b. Command not found

```bash
bash: mongo: command not found
```

If mongo command is not found, see the [installation guide](../installation.md) and install MongoDB.

##### c. Connection refused

```bash
MongoDB shell version v4.2.6
connecting to: mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb
2020-08-31T11:34:18.484+0900 E  QUERY    [js] Error: couldn't connect to server 127.0.0.1:27017, connection attempt failed: SocketException: Error connecting to 127.0.0.1:27017 :: caused by :: Connection refused :
2020-08-31T11:34:18.485+0900 F  -        [main] exception: connect failed
2020-08-31T11:34:18.485+0900 E  -        [main] exiting with code 1
```

If an error is output and startup is not possible, MongoDB instance has not been started with the specified IP address or port number.<br>
See the [MongoDB documentation](https://docs.mongodb.com/manual/reference/configuration-options/#net-options) to set the configuration correctly and restart MongoDB instance.


