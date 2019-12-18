# Database demonstration

## Requirements
Install the following required packages:

- Python3 & modules
- MongoDB
- influxDB & viewer(Grafana)
- YARR SW
- Local DB Tools
- Some other packages (cmake3, gcc, gnuplot, tex script, ghostscript...)

Please follow the procedure below to install them:

- [For centOS](#centos)
- [For macOS](#macos)
- [For Ubuntu](#ubuntu)
- [For Windows](#windows)

### centOS

**version > 7**

```
git clone -b devel https://gitlab.cern.ch/YARR/localdb-tools.git
cd localdb-tools/setting
./db_server_install.sh
```

### macOS

**version > 10.14**

please follow [this page](https://gitlab.cern.ch/YARR/localdb-tools/blob/devel/SETUP.md)

### Ubuntu

**version > 16.04**

```
wget https://gitlab.cern.ch/YARR/localdb-tools/raw/devel/setting/ubuntu/installer_ubuntu.sh
bash installer_ubuntu.sh all
```
This will take about 1 h.

optional, you can specify install packages. e.g. `bash installer_ubuntu.sh gcc7 yarr`


### Windows

Need a **virtual machine** (CentOS or Ubutnu), or enable Windows Subsystem for Linux (WSL) and intall ubuntu

Then, please follow CentOS/Ubuntu instruction.
