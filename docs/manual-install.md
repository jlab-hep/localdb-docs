# Manual Installation

- [yum packages](#yum-packages)
- [python packages](#python-packages)
- [Mongo DB](#mongo-db)

Check [Automatic Installation](automatic-install.md) to install requirements automatically on **centOS7**.

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
$ sudo yum install gnuplot texlive-epstopdf ghostscript
```

### Python packages

- python3

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
itkdb
```

### Mongo DB

- MongoDB version 4.2 or higher for Local DB

For centOS7, you can install/upgrade MongoDB by `localdb-tools/scripts/shell/upgrade_mongoDB_centos.sh`. <br>
Check [MongoDB 4.X Community Edition](https://docs.mongodb.com/manual/installation/) to install and start mongod service on other platform.

```bash
# 0. Check
$ mongo --version
-bash: mongo: command not found

# 1. Install/Upgrade for centOS7
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
