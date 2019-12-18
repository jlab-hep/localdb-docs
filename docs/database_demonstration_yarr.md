# YARR

## Goal

Run the emulator for FE-I4B and upload the test results into Local DB ([MongoDB](database_demonstration_mongodb.md)).

## Pre Requirements

### Required Packages

There are some requirements for compiling YARR SW, <br>
so please check [the requirements](database_demonstration_requirements.md) and be sure to install them.

### MongoDB

You need to start MongoDB service, <br>
so please check [MongoDB](database_demonstration_mongodb.md) to check if the service is running.

## Getting start

### 1. Clone YARR SW

Clone YARR SW repostiroty if you doesn't have YARR SW yet.<br>
**Recommend: use 'devel-localdb' branch in the demonstration**

```bash
$ git clone https://gitlab.cern.ch/YARR/YARR.git
$ cd YARR
$ git checkout devel-localdb
```

### 2. Compile YARR SW

Compile YARR SW if you didn't compile yet.<br>
First please make build directory.

```bash
$ cd YARR
$ mkdir build && cd build
```

Next CMake in the build directory.

- for centOS7

```bash
$ cmake3 ../
```

- for ubuntu

```bash
$ cmake ../ -DCMAKE_CXX_COMPILER=g++-7
```

- for macOS

```bash
$ cmake ../ -DCMAKE_TOOLCHAIN_FILE=../cmake/macos-clang
```

Finaly make & install the binary command to bin directory.

```bash
$ make -j4
$ make install
```

### 3. Run the Emulator

Just type the following command to run the emulator.

```bash
$ cd ../
### pwd ---> path/to/YARR
$ ./bin/scanConsole \
-c configs/connectivity/example_fei4b_setup.json \
-r configs/controller/emuCfg.json \
-s configs/scans/fei4/std_digitalscan.json \
-p
<some texts>
Finishing run: 5840
./data/last_scan/JohnDoe_EnMask.png
./data/last_scan/JohnDoe_L1Dist.pdf
./data/last_scan/JohnDoe_OccupancyMap.png
```

You can check some plots in 'data/last_scan'

### 4. Run the emulator with uploading to Local DB

First you have to prepare the config file for Local DB by 'setup_db.sh'<br>
In this step, you have to set the editor command (e.g. vim, emacs) if the environmental variable 'EDITOR' has not registered.

```bash
$ cd ../
### pwd ---> path/to/YARR
$ cd localdb
$ ./setup_db.sh
<some steps>
[LDB] More detail:
[LDB]   Access 'https://localdb-docs.readthedocs.io/en/master/'
```

And Run the emulator with option '-W' to upload the test data into Local DB.

```bash
$ ./bin/scanConsole \
-c configs/connectivity/example_fei4b_setup.json \
-r configs/controller/emuCfg.json \
-s configs/scans/fei4/std_digitalscan.json \
-W
<some texts>
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017/localdb
#DB INFO# ---> Connection is GOOD.
#DB INFO# -----------------------
#DB INFO# Uploading in the back ground. (log: ~/.yarr/localdb/log/)
```

You can the upload status in the log file '~/.yarr/localdb/log/DAY.log'.<br>
You can also check the data by accessing to [http://127.0.0.1:5000/localdb/](http://127.0.0.1:5000/localdb/) on the machine's browser where Viewer Application is running.<br>
Check [here](database_demonstration_viewer.md) to go to the steps for checking the Viewer Application.

Finish!

## More Detail

Check [YARR Docs](https://yarr.readthedocs.io/en/latest/) for more detail.
