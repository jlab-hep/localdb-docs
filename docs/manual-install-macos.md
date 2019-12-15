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
$ brew install gcc

# 2. Confirm
$ g++ --version
g++ (Homebrew GCC 9.2.0_2) 9.2.0
```

- cmake3 for YARR SW installation

```bash
# 0. Check
$ cmake --version
-bash: cmake: command not found

# 1. Install
$ brew install cmake

# 2. Confirm
$ cmake --version
cmake version 3.12.4
```

- Other dependencies for YARR SW installation

```bash
$ brew install gnuplot
$ brew install epstopdf
$ brew install ghostscript
```

### Python packages

- python3 version 3.4 or higher

```bash
# 0. Check
$ python3 --version
-bash: python3: command not found

# 1. Install
$ brew install python3

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

Check [MongoDB 4.X Community Edition](https://docs.mongodb.com/manual/installation/) to get more detail about installation and starting mongod service.

```bash
# 0. Check
$ mongo --version
-bash: mongo: command not found

# 1. Install/Upgrade for centOS7
$ brew tap mongodb/brew
$ brew install mongodb-community@4.2
$ brew services start mongodb-community@4.2

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
