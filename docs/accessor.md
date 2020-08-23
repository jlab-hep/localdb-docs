# DB Accessor

The **DB Accessor** is to easy handle Local DB.<br>
You can upload local data to Local DB or download data locally from Local DB easily by using this command.

Contents:

1. [Command](#1-command)
2. [Getting Start](#2-getting-start)
3. [FAQ](#3-faq)

## 1. Command

- Location: **YARR/bin/dbAccessor**
- Syntax:

```bash
$ cd YARR
$ ./bin/dbAccessor <-command> [-option]
```

- Commands:
    - [dbAccessor -N](accessor-n.md): Check the connection to Local DB
    - [dbAccessor -S](accessor-s.md): Upload scan data from scan result directory into Local DB
    - [dbAccessor -E](accessor-e.md): Upload DCS data from data files into Local DB
    - [dbAccessor -F](accessor-f.md): Upload DCS data from influxDB into Local DB
    - [dbAccessor -R](accessor-r.md): Upload scan/DCS data recorded in cache into Local DB
    - [dbAccessor -D](accessor-d.md): Retrieve scan data from Local DB
    - [dbAccessor -C](accessor-c.md): Register non-QC componnet data into Local DB

## 2. Getting start

#### 0. Install & Setup

The DB Accessor is included as part of [YARR SW](https://gitlab.cern.ch/YARR/YARR).<br>
Follow the [installation tutorial](requirements.md) to install required packages and make sure to build YARR SW:

```bash
$ cd YARR
$ mkdir build && cd build
$ cmake3 ../
$ make -j4
```

And make sure to setup Local DB configuration files using [YARR/localdb/setup_db.sh](setup-db.md) shell:

```bash
$ cd YARR
$ ./localdb/setup_db.sh
```

#### 1. Confirmation

You can run the [DB Accessor](accessor.md) with command-line option **-N** to check if the command is working and the connection to Local DB is good:

```bash
$ ./bin/dbAccessor -N
```

## 3. [FAQ](accessor-faq.md)
