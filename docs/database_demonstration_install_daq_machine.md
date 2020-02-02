## Installation of the DAQ machine
For centos7<br>
Setup the DAQ machine environment in this page. <br>
<span style="color: red; ">**Use another shell than the DB machine's one and check if you are in local.**</span>

### yum packages
- g++ version 7.0 or higher<br>
```bash
$ sudo yum install -y centos-release-scl
$ sudo yum install -y devtoolset-7
$ source /opt/rh/devtoolset-7/enable
```

- cmake3
```bash
$ sudo yum install -y epel-release
$ sudo yum install -y cmake3
```

- Other dependencies

```bash
$ sudo yum install -y git screen emacs gnuplot texlive-epstopdf ghostscript
```

### Python packages

- python3 version 3.6 or higher

```bash
$ python3 --version
Python 3.6.8
```

- python pip packages

```bash
$ sudo python3 -m pip install arguments coloredlogs pdf2image Pillow pymongo python-dateutil PyYAML pytz matplotlib numpy requests tzlocal influxdb pandas
```
### Yarr SW
Install and compile "Yarr" with bellow commands:

```bash
$ cd ~/work
$ git clone https://gitlab.cern.ch/YARR/YARR.git -b devel-localdb
$ cd YARR
$ mkdir -p build && cd build
$ cmake3 ../
$ make -j4
$ make install
```

Go to next step.<br>
[Download module ID infos](database_demonstration_download_itkpd.md)<br>
