## Base System
* Storage System
  * MongoDB v4.X ([Installation](https://docs.mongodb.com/manual/installation/))
* Read-out System
  * YARR ([Installation](https://yarr.readthedocs.io/en/latest/install/))
* DB Handle System
  * Local DB Tools ([Installation]())

## MongoDB Quick Tutorial

* Check the connection to Mongo DB in mongo shell

```
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

## YARR System Quick Tutorial

* Check the ScanConsole

The ScanConsole is the main read-out program. <br>
Ensure that YARR SW is installed before running the ScanConsole. ([YARR SW Installation](https://yarr.readthedocs.io/en/latest/install/))

```
$ cd <YARR SW installation dir>
$ bin/scanConsole -r configs/controller/emuCfg.json -c configs/connectivity/example_fei4b_setup.json -s configs/scans/fei4/std_digitalscan.json -p
```

This runs a digitalscan with the FE-I4B emulator. This does not use or require any hardware and will run purely in software.

## Local DB Tools Quick Tutorial

* Check Uploader

a

* Check Retriever

a

* Check Viewer Application

a

* Check Synchronization

a

* Check Archive 

a
