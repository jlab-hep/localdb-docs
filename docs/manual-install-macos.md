# Manual Installation for macOS

You can install the [requirements for the system](requirements-list.md) on macOS manually following this page.<br>
If you want to install on centOS7, see the [manual installation guide for centOS7](manual-install.md).

- [Installation for DAQ machine](#installation-for-daq-machine)
    - [brew packages](#brew-packages-daq)
        - brew command
        - g++
        - cmake3
        - other dependencies
    - [python packages](#python-packages-daq)
        - python3
        - pip modules
    - [YARR SW Compilation](#yarr-sw-compilation)
- [Installation for DB machine](#installation-for-db-machine)
    - [brew packages](#brew-packages-db)
        - brew command
        - g++
        - cmake3
        - other dependencies
    - [python packages](#python-packages-db)
        - python3
        - pip modules
    - [Local DB tools Compilation](#localdb-tools-compilation)
    - [MongoDB](#mongodb)
    - [influxDB](#influxdb)
    - [Grafana](#grafana)
    - [ROOT](#root)

## Installation for DAQ machine

### brew packages (DAQ)

#### brew command

**1. Check**

```bash
$ brew --version
-bash: brew: command not found
```

**2. Install**

```bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

**3. Confirm**

```bash
$ brew --version
Homebrew 2.2.1
...
```

#### g++

It requires g++ version 7.0 or higher for YARR SW compilation.

**1. Check**

```bash
$ g++ --version
-bash: g++: command not found
```

**2. Install**

```bash
$ brew install gcc
```

**3. Confirm**

```bash
$ g++ --version
g++ (Homebrew GCC 9.2.0_2) 9.2.0
```

#### cmake3

It requires cmake version 3 for YARR SW compilation.

**1. Check**

```bash
$ cmake --version
-bash: cmake: command not found
```

**2. Install**

```bash
$ brew install cmake
```

**3. Confirm**

```bash
$ cmake --version
cmake version 3.12.4
```

#### Other dependencies

It requires several other packages for YARR SW compilation.

**Install**

```bash
$ brew install gawk
$ brew install gnuplot
$ brew install ghostscript
```

And you need to install MacTex to output the plots of the scan results proparely.

### Python packages (DAQ)

#### python3

It requires python version 3.6 or higher for Local DB tools compilation.

**1. Check**

```bash
$ python3 --version
-bash: python3: command not found
```

**2. Install**

```bash
$ brew install python3
```

**3. Confirm**

```bash
$ python3 --version
Python 3.6.8
```

#### pip modules

It requires several pip modules for Local DB tools compilation.

**Install**

```bash
$ sudo python3 -m pip install \
arguments \
coloredlogs \
Flask \
Flask-PyMongo \
Flask-HTTPAuth \
Flask-Mail \
pdf2image \
Pillow \
prettytable \
pymongo \
python-dateutil \
PyYAML \
pytz \
plotly \
matplotlib \
numpy \
requests \
tzlocal \
itkdb \
influxdb \
pandas
```

### YARR SW Compilation

It requires to compile [YARR](https://gitlab.cern.ch/YARR/YARR) in working directory of your DAQ machine to scan ASICs.<br>
If you have not clone the repository of YARR, see the [clone git repository for the pre installation](installation.md) to do it.

```bash
$ cd path/to/YARR
$ mkdir build && cd build
$ cmake3 ..  -DCMAKE_TOOLCHAIN_FILE=../cmake/macos-clang
$ make -j4
$ make install
```

Once the compile is successful, the binary commands are placed in **YARR/bin**.

## Installation for DB machine

### brew packages (DB)

#### brew command

**1. Check**

```bash
$ brew --version
-bash: brew: command not found
```

**2. Install**

```bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

**3. Confirm**

```bash
$ brew --version
Homebrew 2.2.1
...
```

#### g++

It requires g++ version 7.0 or higher for Local DB tools compilation.

**1. Check**

```bash
$ g++ --version
-bash: g++: command not found
```

**2. Install**

```bash
$ brew install gcc
```

**3. Confirm**

```bash
$ g++ --version
g++ (Homebrew GCC 9.2.0_2) 9.2.0
```

#### cmake3

It requires cmake version 3 for Local DB tools compilation.

**1. Check**

```bash
$ cmake --version
-bash: cmake: command not found
```

**2. Install**

```bash
$ brew install cmake
```

**3. Confirm**

```bash
$ cmake --version
cmake version 3.12.4
```

#### Other dependencies

It requires several other packages for Local DB tools compilation.

**Install**

```bash
$ brew install gawk
```

### Python packages (DB)

#### python3

It requires python version 3.6 or higher for Local DB tools compilation.

**1. Check**

```bash
$ python3 --version
-bash: python3: command not found
```

**2. Install**

```bash
$ brew install python3
```

**3. Confirm**

```bash
$ python3 --version
Python 3.6.8
```

#### pip modules

It requires several pip modules for Local DB tools compilation.

**Install**

```bash
$ sudo python3 -m pip install \
arguments \
coloredlogs \
Flask \
Flask-PyMongo \
Flask-HTTPAuth \
Flask-Mail \
pdf2image \
Pillow \
prettytable \
pymongo \
python-dateutil \
PyYAML \
pytz \
plotly \
matplotlib \
numpy \
requests \
tzlocal \
itkdb \
influxdb \
pandas
```

### LocalDB tools Compilation

It requires to compile [Local DB tools](https://gitlab.cern.ch/YARR/localdb-tools) in working directory of your DB machine to handle Local DB.<br>
If you have not clone the repository of Local DB tools, see the [clone git repository for the pre installation](installation.md) to do it.

### MongoDB

It requires MongoDB version 4.2 or higher for Local DB.<br>
See [MongoDB 4.X Community Edition](https://docs.mongodb.com/manual/installation/) to get more information.

**1. Check**

```bash
$ mongo --version
-bash: mongo: command not found
```

**2. Install/Upgrade**

```
$ brew tap mongodb/brew
$ brew install mongodb-community@4.2
$ brew services start mongodb-community@4.2
```

**3. Configm**

```bash
$ mongo # If port is different from 27017, need to put option as "--port <port number>"
MongoDB shell version v4.2.1
...
> db
test
> exit
bye
```

If you catch the message **"exception: connect failed"**, you should check that MongoDB is running.

## influxDB

It requires influxDB to manage DCS data.

**1. Check**

```bash
$ influx --version
-bash: mongo: command not found
```

**2. Install**

```bash
$ brew install influxdb
$ ln -sfv /usr/local/opt/influxdb/*.plist ~/Library/LaunchAgents
$ launchctl load ~/Library/LaunchAgents/homebrew.mxcl.influxdb.plist
```

**3. Confirm**

```bash
$ influx # If port is different from 27017, need to put option as "--port <port number>"
Connected to http://localhost:8086 version 1.7.9
InfluxDB shell version: 1.7.9
...
> exit
```

### Grafana

**1. Check**

```bash
$ grafana-server -v
-bash: grafana-server: command not found
```

**2. Install**

```bash
$ brew install grafana
$ brew tap homebrew/services
$ brew services start grafana
```

**3. Install**

```bash
$ grafana-server -v
Version 6.5.2 (commit: 742d165, branch: HEAD)
```

See [Grafana Installation](https://grafana.com/docs/grafana/latest/installation/requirements/) to get more detail.

### Root

It requires ROOT version 6.18 or higher to display plots on the viewer application.<br>
See [ROOT Installation](https://root.cern/install/) to get more detail.
