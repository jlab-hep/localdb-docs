## Installation for the DB machine
### yum packages
- g++ version 7.0 or higher
```bash
$ yum install centos-release-scl
...
$ yum install devtoolset-7
...
$ source /opt/rh/devtoolset-7/enable
$ g++ --version
g++ (GCC) 7.3.1 20180303 (Red Hat 7.3.1-5)
```

- cmake3

```bash
$ yum install epel-release
...
$ yum install cmake3
...
$ cmake3 --version
cmake3 version 3.14.6
...
```

- Other dependencies
```bash
$ sudo yum install git emacs
```

### Python packages

- python3 version 3.6 or higher

```bash
$ python3 --version
Python 3.6.8
```

- python pip packages
```bash
# 1. Install
$ python3 -m pip install arguments coloredlogs Flask Flask-PyMongo Flask-HTTPAuth Flask-Mail pdf2image Pillow prettytable pymongo python-dateutil PyYAML pytz plotly matplotlib numpy requests tzlocal itkdb influxdb pandas
```

### LocalDB tools

```bash
$ cd ~/work
$ git clone https://gitlab.cern.ch/YARR/localdb-tools.git
$ cd localdb-tools
$ git checkout devel
```

### Mongo DB

- MongoDB version 4.2 or higher for Local DB
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

Success! Upgraded MongoDB version to 4.2!
You can check it by 'mongo --version'
Enjoy!

# 2. Confirm
$ mongo
MongoDB shell version v4.2.1
...
> db
test
> exit
bye
```
### influxDB

```bash
$ cat <<EOF | sudo tee /etc/yum.repos.d/influxdb.repo
[influxdb]
name = InfluxDB Repository - RHEL \$releasever
baseurl = https://repos.influxdata.com/rhel/\$releasever/\$basearch/stable
enabled = 1
gpgcheck = 1
gpgkey = https://repos.influxdata.com/influxdb.key
EOF
$ yum install influxdb
$ systemctl start influxdb
$ influx
Influx DB shell version X.X.X
>
```
### Grafana

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
$ yum install grafana
$ systemctl start grafana-server
$ grafana-server -v
Version 6.5.2 (commit: 742d165, branch: HEAD)
```

Check [Grafana Installation](https://grafana.com/docs/grafana/latest/installation/requirements/) for more detail.


### Root

```bash
$ yum install git cmake gcc-c++ gcc binutils libX11-devel libXpm-devel libXft-devel libXext-devel
$ yum install gcc-gfortran openssl-devel pcre-devel mesa-libGL-devel mesa-libGLU-devel glew-devel ftgl-devel mysql-devel fftw-devel cfitsio-devel graphviz-devel avahi-compat-libdns_sd-devel python-devel libxml2-devel giflib wget
$ cd /opt
$ wget https://root.cern/download/root_v6.18.04.Linux-centos7-x86_64-gcc4.8.tar.gz
$ tar zxf root_v6.18.04.Linux-centos7-x86_64-gcc4.8.tar.gz
$ source /opt/root/bin/thisroot.sh
```
