# Installation for macOS

## version

**version > 10.14**

## Brew install

```bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## Install other functions

```bash
$ brew install gawk
$ brew install python3
$ brew install cmake
$ brew install gcc
$ brew install gnuplot
$ (brew cask install mactex)
$ brew install ghostscript
```

## python3 module install (pip3 install "module name")

```bash
$ python3 -m piip install \
influxdb \
datetime \
time \
json \
dateutil \
pillez \
pandas \
argparse \
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
```

## mongo install

```bash
$ brew tap mongodb/brew
$ brew install mongodb-community@4.2
$ brew services start mongodb-community@4.2
$ ps aux | grep -v grep | grep mongod
```

## influxDB install

```bash
$ brew install influxdb
$ ln -sfv /usr/local/opt/influxdb/*.plist ~/Library/LaunchAgents
$ launchctl load ~/Library/LaunchAgents/homebrew.mxcl.influxdb.plist
```

## Grafana install

```bash
$ brew install grafana
$ brew tap homebrew/services
$ brew services start grafana
```

## iStats install

```bash
$ sudo gem install iStats
```

## Yarr install

```bash
$ git clone https://gitlab.cern.ch/Yarr/Yarr.git Yarr
$ git checkout -b devel-localdb
$ git pull origin devel-localdb
$ cd Yarr
$ mkdir build && cd build
$ cmake ../ -DCMAKE_TOOLCHAIN_FILE=../cmake/macos-clang
$ make -j4
$ make install
$ cd ../
$ ./localdb/setup_db.sh
```

## localdb-tools setup

It is better to put "localdb-tools" directry in the same level as Yarr directry.

```bash
$ git clone https://gitlab.cern.ch/YARR/localdb-tools.git
$ cd localdb-tools
$ git checkout devel 
```

## dummy temperature install

```bash
$ git clone https://gitlab.cern.ch/syamagay/influxdb_tools.git
$ cd influxdb_tools
$ git checkout devel
```
