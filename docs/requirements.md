# Pre Requirements for Local DB System

## Base System
* Storage System: Mongo DB v4.X
    * [Installation](#mongodb-installation)
    * [Confirmation](#mongodb-confirmation)
* Read-out System: YARR
    * [Installation](#yarr-installation)
    * [Confirmation](#yarr-confirmation)

## MongoDB Installation

Please look at [MongoDB Documentation](https://docs.mongodb.com/manual/installation/) to install MongoDB 4.X Community Edition and start mongod service.

## MongoDB Confirmation

* Check the connection to Mongo DB in mongo shell

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

## YARR Installation

Please look at [YARR Docs](https://yarr.readthedocs.io/en/latest/install/) to install YARR System and setup.

## YARR Confirmation

* Check the ScanConsole

The ScanConsole is the main read-out program. <br>
Ensure that YARR SW is installed before running the ScanConsole. ([YARR SW Installation](https://yarr.readthedocs.io/en/latest/install/))

```bash
$ cd <YARR SW installation dir>
$ bin/scanConsole -r configs/controller/emuCfg.json -c configs/connectivity/example_fei4b_setup.json -s configs/scans/fei4/std_digitalscan.json -p
```

This runs a digitalscan with the FE-I4B emulator. This does not use or require any hardware and will run purely in software.
