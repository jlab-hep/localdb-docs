# Quick Tutorial

You can handle Local DB (e.g. store result data by YARR) following the tutorial.

### Setup

First please be sure to build YARR SW. <br>

```bash
$ cd YARR
$ (git checkout devel-localdb)
$ mkdir build && cd build
# for linux
$ cmake3 ../                                             
# for macOS
$ cmake ../ -DCMAKE_TOOLCHAIN_FILE=../cmake/macos-clang 
$ make -j4
$ make install
```
> [More detail about YARR SW](https://yarr.readthedocs.io/en/latest/)

And please be sure to setup Local DB setting using `setup_db.sh`. <br>
This script confirms if the python packages is satisfied, the default config files are prepared, the commands are enabled, and the DB connection is established. <br>

```bash
$ cd ../
$ ./localdb/setup_db.sh
```
> [More detail about setup_db.sh](setup-db.md)


## [Basic Tutorial](basic-tutorial.md)

Contents:

1. Scan and Upload data into Local DB
2. Retrieve data from Local DB

## [Advanced Tutorial](advanced-tutorial.md)

Contents:

- a. Setup Web application of Local DB (Viewer Application)
- b. Register component data into Local DB
- c. Retrieve component data from ITkPD into Local DB (ITkPD Interface)
- d. Scan and Upload data associated with the component data into Local DB
- e. Register DCS data associated with the test data
- f. Share data with the other Local DB (Synchronization Tool)
- g. Back-up Local DB (Archive Tool)

## Local DB Tools Details

- [Upload Tool](upload.md)
- [Retrieve Tool](retrieve.md)
- [Viewer Application](viewer.md)
- [Sycnhronization Tool](sync.md)
- [Archive Tool](archive.md)
- [ITk PD Interface](itkpd-interface.md)
- [DB Accessor](accessor.md)
- [scanConsole](scanconsole.md)
