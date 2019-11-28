# Automatic Installation

**For centOS7**, `YARR/localdb/db_yarr_install.sh`/`localdb-tools/setting/db_server_install.sh` can

- Check missing packages
- Install requirements for DAQ/DB Machine
- Enable MongoDB
- Confirme the installation status & Show quick tutorial

Check [Manual Installation](manual-install.md) to install requirements on other platform.

## scripts

- [db_yarr_install.sh](#a-db_yarr_installsh) (For DAQ machine)
- [db_server_install.sh](#b-db_server_installsh) (For DB server)

### a) db_yarr_install.sh

```bash
$ git clone https://gitlab.cern.ch/YARR/YARR.git
$ git checkout devel
$
$ cd YARR/localdb
$ ./db_yarr_install.sh
[LDB] Looking for missing packages for Local DB and Tools ...
[LDB] Done.
------------------------------------
          Missing packages
------------------------------------
## Show packages to be installed ##
 yum    : centos-release-scl.noarch
  .
  .
  .
 python : arguments
  .
  .
  .
------------------------------------
[LDB] Install these package? [y/n]
y

[LDB] Following steps will be done ...
[LDB] - Install required packages by yum & pip.
[LDB]
[LDB] You need to be root to perform this command.
[sudo] password for dbuser: XXXXXXX
[LDB] OK!

< Installing packages with many texts >

[LDB] Final confirming ...
[LDB] Success!!
----------------------------------------
Enjoy!!
```

### b) db_server_install.sh

```bash
$ git clone https://gitlab.cern.ch/YARR/localdb-tools.git
$ git checkout devel
$
$ cd localdb-tools/setting
$ ./db_server_install.sh
[LDB] Looking for missing packages for Local DB and Tools ...
[LDB] Done.
------------------------------------
          Missing packages
------------------------------------
## Show packages to be installed ##
 yum    : centos-release-scl.noarch
  .
  .
  .
 python : arguments
  .
  .
  .
------------------------------------
[LDB] Install these package? [y/n]
y

[LDB] Following steps will be done ...
[LDB] - Install required packages by yum & pip.
[LDB]
[LDB] You need to be root to perform this command.
[sudo] password for dbuser: XXXXXXX
[LDB] OK!

< Installing packages with many texts >

[LDB] Final confirming ...
[LDB] Success!!
----------------------------------------
Enjoy!!
```


