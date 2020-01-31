### yum packages

- g++ version 7.0 or higher for YARR SW installation

```bash
$ sudo yum install centos-release-scl
$ sudo yum install devtoolset-7

$ source /opt/rh/devtoolset-7/enable
$ g++ --version
g++ (GCC) 7.3.1 20180303 (Red Hat 7.3.1-5)
```

- cmake3 for YARR SW installation
```bash
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
matplotlib \
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
$ git checkout devel-localdb
$ mkdir build && cd build
$ cmake3 ../
$ make -j4
$ make install
```

