# Manual Installation

- [yum packages](#yum-packages)
- [python packages](#python-packages)
- [Mongo DB](#mongo-db)

Check [Automatic Installation](automatic-install.md) to install requirements automatically on **centOS7**.

## DAQ machine
### yum packages

- g++ version 7.0 or higher for YARR SW installation

```bash
# 0. Check
$ g++ --version
-bash: g++: command not found

# 1. Install
$ sudo yum install centos-release-scl
$ sudo yum install devtoolset-7

# 2. Confirm
$ source /opt/rh/devtoolset-7/enable
$ g++ --version
g++ (GCC) 7.3.1 20180303 (Red Hat 7.3.1-5)
```

- cmake3 for YARR SW installation

```bash
# 0. Check
$ cmake3 --version
-bash: cmake3: command not found

# 1. Install
$ sudo yum install epel-release
$ sudo yum install cmake3

# 2. Confirm
$ cmake3 --version
cmake3 version 3.14.6
```

- Other dependencies for YARR SW installation

```bash
$ sudo yum install git
```
```bash
$ sudo yum install screen
```
```bash
$ sudo yum install gnuplot texlive-epstopdf ghostscript
```

### Python packages

- python3 version 3.6 or higher

```bash
# 0. Check
$ python3 --version
-bash: python3: command not found

# 1. Install
$ sudo yum install epel-release
$ sudo yum install python3.x86_64

# 2. Confirm
$ python3 --version
Python 3.6.8
```

- python pip packages

```bash
# 1. Install
$ sudo python3 -m pip install \
arguments \
coloredlogs \
pdf2image \
Pillow \
pymongo \
python-dateutil \
PyYAML \
pytz \
numpy \
requests \
tzlocal \
influxdb \
pandas
```
### Yarr SW
Install and compile "Yarr" in working directry of your DAQ machine with bellow commands:

```bash
$ git clone https://gitlab.cern.ch/YARR/YARR.git
$ cd YARR
$ (git checkout devel-localdb)
$ cd YARR
$ mkdir build && cd build
$ cmake3 ../
$ make -j4
$ make install
```

## DB machine
### yum packages

- g++ version 7.0 or higher

```bash
# 0. Check
$ g++ --version
-bash: g++: command not found

# 1. Install
$ sudo yum install centos-release-scl
$ sudo yum install devtoolset-7

# 2. Confirm
$ source /opt/rh/devtoolset-7/enable
$ g++ --version
g++ (GCC) 7.3.1 20180303 (Red Hat 7.3.1-5)
```

- cmake3

```bash
# 0. Check
$ cmake3 --version
-bash: cmake3: command not found

# 1. Install
$ sudo yum install epel-release
$ sudo yum install cmake3

# 2. Confirm
$ cmake3 --version
cmake3 version 3.14.6
```

- Other dependencies
```bash
$ sudo yum install git
```
```bash
$ sudo yum install screen
```

### Python packages

- python3 version 3.6 or higher

```bash
# 0. Check
$ python3 --version
-bash: python3: command not found

# 1. Install
$ sudo yum install epel-release
$ sudo yum install python3.x86_64

# 2. Confirm
$ python3 --version
Python 3.6.8
```

- python pip packages

```bash
# 1. Install
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

### LocalDB tools
Install "localdb-tools" in working directry of your DB machine with bellow commands:

```bash
$ git clone https://gitlab.cern.ch/YARR/localdb-tools.git
$ (git checkout devel)
```

### Mongo DB

- MongoDB version 4.2 or higher for Local DB

For **centOS7**, you can install/upgrade MongoDB by `localdb-tools/scripts/shell/upgrade_mongoDB_centos.sh`. <br>
Check [MongoDB 4.X Community Edition](https://docs.mongodb.com/manual/installation/) to install and start mongod service on other platform.

```bash
# 0. Check
$ mongo --version
-bash: mongo: command not found

# 1. Install/Upgrade
$ cd localdb-tools/scripts/shell
$ ./upgrade_mongoDB_centos.sh
[sudo] password for dbuser: XXXXXXX
OK!

----------------------------------------------
[WARNING] MongoDB version 4.2 or greater is required
----------------------------------------------

Install MongoDB version 4.2? [y/n]
y

< Installing packages with many texts >

Success! Upgraded MongoDB version to 4.2!
You can check it by 'mongo --version'
Enjoy!

# 2. Confirm
$ mongo [--port <port number>]
MongoDB shell version v4.2.1
...
> db
test
> exit
bye
```

If you catch the message **"exception: connect failed"**, you should check that MongoDB is running.

### influxDB

```bash
# 0. Check
$ influx --version
-bash: influx: command not found

# 1. Install
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

# 2. Confirm
$ influx
Influx DB shell version X.X.X
>
```

Check [influxDB Installation](https://docs.influxdata.com/influxdb/v1.7/introduction/installation/) for more detail.

### Grafana

```bash
# 0. Check
$ grafana-server -v
-bash: grafana-server: command not found

# 1. Install
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

# 2. Confirm
$ grafana-server -v
Version 6.5.2 (commit: 742d165, branch: HEAD)
```

Check [Grafana Installation](https://grafana.com/docs/grafana/latest/installation/requirements/) for more detail.


