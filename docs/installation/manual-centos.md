# Manual Installation for centOS7

You can install the [requirements for the system](requirements-list.md) on centOS7 manually following this page.<br>
If you want to install on macOS, see the [manual installation guide for macOS](manual-macos.md).

### Table of Contents

- [Installation for DAQ machine](#installation-for-daq-machine)
    - [yum packages](#yum-packages-daq)
        - g++
        - cmake3
        - Other dependencies
    - [python packages](#python-packages-daq)
        - python3
        - pip modules
    - [YARR SW Compilation](#yarr-sw-compilation)
- [Installation for DB machine](#installation-for-db-machine)
    - [yum packages](#yum-packages-db)
        - g++
        - cmake3
        - Other dependencies
    - [python packages](#python-packages-db)
        - python3
        - pip modules
    - [Local DB tools Compilation](#localdb-tools-compilation)
    - [MongoDB](#mongodb)
    - [influxDB](#influxdb)
    - [Grafana](#grafana)
    - [ROOT](#root)

---

## Installation for DAQ machine

### yum packages (DAQ)

#### g++

It requires g++ version 7.0 or higher for YARR SW compilation.

```bash
$ sudo yum install centos-release-scl
$ sudo yum install devtoolset-7
$ source /opt/rh/devtoolset-7/enable
$ g++ --version
g++ (GCC) 7.3.1 20180303 (Red Hat 7.3.1-5)
```

#### cmake3

It requires cmake version 3 for YARR SW compilation.

```bash
$ sudo yum install epel-release
$ sudo yum install cmake3
$ cmake3 --version
cmake3 version 3.14.6
```

#### Other dependencies

It requires several other packages for YARR SW compilation.

```bash
$ sudo yum install git screen gnuplot texlive-epstopdf ghostscript
```

### Python packages (DAQ)

#### python3

It requires python version 3.6 or higher for Local DB tools compilation.

```bash
$ sudo yum install epel-release
$ sudo yum install python3.x86_64
$ python3 --version
Python 3.6.8
```

#### pip modules

It requires several pip modules for Local DB tools compilation.

```bash
$ sudo python3 -m pip install \
arguments \
coloredlogs \
pdf2image \
Pillow \
pymongo \
python-dateutil \
PyYAML \
pytz \
matplotlib \
numpy \
requests \
tzlocal \
influxdb \
pandas
```

### YARR SW Compilation

It requires to compile [YARR](https://gitlab.cern.ch/YARR/YARR) in working directory of your DAQ machine to scan ASICs.<br>
If you do not have the repository of YARR, see the [clone git repository for the pre installation](../installation.md).

```bash
$ cd path/to/YARR
$ mkdir build && cd build
$ cmake3 ../
$ make -j4
$ make install
```

Once the compile is successful, the binary commands are placed in **YARR/bin**.

---

## Installation for DB machine

### yum packages (DB)

#### g++

It requires g++ version 7.0 or higher for Local DB tools compilation.

```bash
$ sudo yum install centos-release-scl
$ sudo yum install devtoolset-7
$ source /opt/rh/devtoolset-7/enable
$ g++ --version
g++ (GCC) 7.3.1 20180303 (Red Hat 7.3.1-5)
```

#### cmake3

It requires cmake version 3 for Local DB tools compilation.

```bash
$ sudo yum install epel-release
$ sudo yum install cmake3
$ cmake3 --version
cmake3 version 3.14.6
```

#### Other dependencies

It requires several other packages for Local DB tools compilation.

```bash
$ sudo yum install git screen
```

### Python packages (DB)

#### python3

It requires python version 3.6 or higher for Local DB tools compilation.

```bash
$ sudo yum install epel-release
$ sudo yum install python3.x86_64
$ python3 --version
Python 3.6.8
```

#### pip modules

It requires several pip modules for Local DB tools compilation.

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
If you do not have the repository of Local DB tools, see the [clone git repository for the pre installation](../installation.md).

### MongoDB

It requires MongoDB version 4.2 or higher for Local DB.<br>
You can run the [upgrade_mongodb_centos.sh](../script/upgrade_mongodb_centos.md) shell to install/upgrade MongoDB on centOS7.

```bash
$ cd localdb-tools/scripts/shell
$ ./upgrade_mongoDB_centos.sh
[sudo] password for dbuser: XXXXXXX
OK!

Install MongoDB version 4.2? [y/n]
y

< Installing packages with many texts >
$ mongo [--port <port number>]
MongoDB shell version v4.2.1
...
> db
test
> exit
bye
```

!!! Note
    See [MongoDB 4.X Community Edition](https://docs.mongodb.com/manual/installation/) to get more detail.

!!! Warning
    If you catch the message **"exception: connect failed"**, you should check that MongoDB is running.

### influxDB

It requires influxDB to manage DCS data.

```bash
$ cat <<EOF | sudo tee /etc/yum.repos.d/influxdb.repo
[influxdb]
name = InfluxDB Repository - RHEL \$releasever
baseurl = https://repos.influxdata.com/rhel/\$releasever/\$basearch/stable
enabled = 1
gpgcheck = 1
gpgkey = https://repos.influxdata.com/influxdb.key
EOF
$ sudo yum install influxdb
$ sudo systemctl start influxdb
$ influx
Influx DB shell version X.X.X
>
```

!!! Note
    See [influxDB Installation](https://docs.influxdata.com/influxdb/v1.7/introduction/installation/) to get more detail.

### Grafana

It requires Grafana to manage data in influxDB.

```bash
$ cat <<EOF | sudo tee /etc/yum.repos.d/grafana.repo
[grafana]
name=grafana
baseurl=https://packages.grafana.com/oss/rpm
repo_gpgcheck=1
enabled=1
gpgcheck=1
gpgkey=https://packages.grafana.com/gpg.key
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
EOF
$ sudo yum install grafana
$ sudo systemctl start grafana-server
$ grafana-server -v
Version 6.5.2 (commit: 742d165, branch: HEAD)
```

!!! Note
    See [Grafana Installation](https://grafana.com/docs/grafana/latest/installation/requirements/) to get more detail.

### Root

It requires ROOT version 6.18 or higher to display plots on the viewer application.

```bash
$ yum install git cmake gcc-c++ gcc binutils \
libX11-devel libXpm-devel libXft-devel libXext-devel
$ yum install gcc-gfortran openssl-devel pcre-devel \
mesa-libGL-devel mesa-libGLU-devel glew-devel ftgl-devel mysql-devel \
fftw-devel cfitsio-devel graphviz-devel \
avahi-compat-libdns_sd-devel libldap-dev python-devel \
libxml2-devel gsl-static giflib wget
$ cd /opt
$ wget https://root.cern/download/root_v6.18.04.Linux-centos7-x86_64-gcc4.8.tar.gz
$ tar zxf root_v6.18.04.Linux-centos7-x86_64-gcc4.8.tar.gz
$ source /opt/root/bin/thisroot.sh
```

!!! Note
    See [ROOT Installation](https://root.cern/install/) to get more detail.
