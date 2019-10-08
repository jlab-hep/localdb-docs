## Storage System: Mongo DB v4.X

Ensure that [MongoDB 4.X Community Edition](https://docs.mongodb.com/manual/installation/) is installed and mongod service is started. <br>
Check the connection to Mongo DB in mongo shell by:

```bash
$ export PATH=$PATH:<mongodb installation dir>/bin
$ mongo [--port <port number>]
MongoDB shell version v4.0.12
...
> db
test
> exit
bye
```

If you catch the message "exception: connect failed", you should check that MongoDB is running.

## Read-out System: YARR

Ensure that [YARR SW](https://yarr.readthedocs.io/en/latest/install/) is installed and set-up. <br>
Check the ScanConsole, which is the main read-out program, working by:

```bash
$ cd <YARR SW installation dir>
$ bin/scanConsole -r configs/controller/emuCfg.json -c configs/connectivity/example_fei4b_setup.json -s configs/scans/fei4/std_digitalscan.json -p
```

This runs a digitalscan with the FE-I4B emulator. This does not use or require any hardware and will run purely in software.
