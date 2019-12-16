# Database demonstration


## Requirements
Install require packages


### CentOS
version > 7

```
git clone -b devel https://gitlab.cern.ch/YARR/localdb-tools.git
cd localdb-tools/setting
./db_server_install.sh
```

### MacOS
version > 10.14

please follow below link.

https://gitlab.cern.ch/YARR/localdb-tools/blob/devel/SETUP.md


### Ubuntu
version > 16.04
```
wget https://gitlab.cern.ch/YARR/localdb-tools/blob/devel/setting/ubuntu/installer_ubuntu.sh
bash installer_ubuntu.sh all
```

optional, you can specify install packages. e.g. `bash installer_ubuntu.sh gcc7 yarr`


### Windows
Need a virtual machine (CentOS or Ubutnu), or enable Windows Subsystem for Linux (WSL) and intall ubuntu

Then, please follow CentOS/Ubuntu instruction.
