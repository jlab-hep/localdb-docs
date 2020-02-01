## Installation for the DAQ machine
For centos7<br>
Setup the DAQ machine environment from here. <br>
<span style="color: red; ">**Change the screen and check if you are in local.**</span>

### yum packages
- g++ version 7.0 or higher<br>
Please answer "y" in all steps.
```bash
$ sudo yum install centos-release-scl
...
$ sudo yum install devtoolset-7
...
$ source /opt/rh/devtoolset-7/enable
$ g++ --version
g++ (GCC) 7.3.1 20180303 (Red Hat 7.3.1-5)
...
```

- cmake3
```bash
$ sudo yum install epel-release
...
$ sudo yum install cmake3
...
$ cmake3 --version
cmake3 version 3.14.6
...
```

- Other dependencies

```bash
$ sudo yum install git screen emacs gnuplot texlive-epstopdf ghostscript
...
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
...
```
### Yarr SW
Install and compile "Yarr" with bellow commands:

```bash
$ cd ~/work
$ git clone https://gitlab.cern.ch/YARR/YARR.git
...
$ cd YARR
$ git checkout devel-localdb
...
$ mkdir build && cd build
$ cmake3 ../
$ make -j4
$ make install
```

Finish installation. Back to the previous page and go to next step.
