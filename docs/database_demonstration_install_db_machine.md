## Installation for the DB machine
For centos7<br>
Setup the DB machine environment from here.

### Connect DB machine via ssh

Please do the following command on your command prompt to connect DB machine via ssh.<br>
We prepared a virtual server and tell you the server name.<br>
**Change the server name according to the given name** (e.g.:root@localdbserver1)<br> 
Default password is "password".

```bash
$ ssh root@localdbserverX
Password: 
Last login: ... 2020 from monkeyisland.dyndns.cern.ch
```
![ssh connection](images/ssh_connection.png)

### yum packages
- g++ version 7.0 or higher<br>
```bash
$ yum install -y centos-release-scl
$ yum install -y devtoolset-7
$ source /opt/rh/devtoolset-7/enable
$ g++ --version
g++ (GCC) 7.3.1 20180303 (Red Hat 7.3.1-5)
...
```

- cmake3

```bash
$ yum install -y epel-release
$ yum install -y cmake3
$ cmake3 --version
cmake3 version 3.14.6
...
```

- Other dependencies
```bash
$ yum install -y git emacs
```

### Python packages

- python3 version 3.6 or higher

```bash
$ python3 --version
Python 3.6.8
```

- python pip packages
```bash
$ python3 -m pip install arguments coloredlogs Flask Flask-PyMongo Flask-HTTPAuth Flask-Mail pdf2image Pillow prettytable pymongo python-dateutil PyYAML pytz plotly matplotlib numpy requests tzlocal itkdb influxdb pandas
```

### LocalDB tools
Tools to operate LocalDB
```bash
$ cd ~/
$ mkdir work && cd work
$ git clone https://gitlab.cern.ch/YARR/localdb-tools.git -b devel
```

### Mongo DB

MongoDB version 4.2 or higher for Local DB<br>
This is a main database to store QC results<br>
**There might be some error masages but please don't worry and go ahead.**
```bash
$ cd ~/work/localdb-tools/scripts/shell
$ ./upgrade_mongoDB_centos.sh
[sudo] password for dbuser: XXXXXXX
OK!

----------------------------------------------
[WARNING] MongoDB version 4.2 or greater is required
----------------------------------------------

Install MongoDB version 4.2? [y/n]
y

< Installing packages with many texts >
...
```
Start mongodb
```bash
$ systemctl start mongod.service
$ mongo
MongoDB shell version v4.2.1
...
> db
test
> exit
bye
```
### influxDB

This is a database to store DCS data<br>
Do the bellow command at once.
```bash
cat <<EOF | sudo tee /etc/yum.repos.d/influxdb.repo
[influxdb]
name = InfluxDB Repository - RHEL \$releasever
baseurl = https://repos.influxdata.com/rhel/\$releasever/\$basearch/stable
enabled = 1
gpgcheck = 1
gpgkey = https://repos.influxdata.com/influxdb.key
EOF
```
Install and Start influxDB
```bash
$ yum install -y influxdb
$ systemctl start influxdb
$ influx
Influx DB shell version X.X.X
> exit
```
### Grafana
This is a web application to see contents of influxdb.<br>
Do the bellow command at once.
```bash
cat <<EOF | sudo tee /etc/yum.repos.d/grafana.repo
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
```

Install and Start influxDB
```bash
$ yum install -y grafana
$ systemctl start grafana-server
$ grafana-server -v
Version 6.6.0 (commit: 742d165, branch: HEAD)
```

### Root
Root SW installation
```bash
$ yum install -y git cmake gcc-c++ gcc binutils libX11-devel libXpm-devel libXft-devel libXext-devel gcc-gfortran openssl-devel pcre-devel mesa-libGL-devel mesa-libGLU-devel glew-devel ftgl-devel mysql-devel fftw-devel cfitsio-devel graphviz-devel avahi-compat-libdns_sd-devel python-devel libxml2-devel giflib wget
$ cd /opt
$ wget https://root.cern/download/root_v6.18.04.Linux-centos7-x86_64-gcc4.8.tar.gz
$ tar zxf root_v6.18.04.Linux-centos7-x86_64-gcc4.8.tar.gz
$ source /opt/root/bin/thisroot.sh
```
Finish installation. Back to the previous page and go to next step.
