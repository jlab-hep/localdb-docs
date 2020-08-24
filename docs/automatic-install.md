# Automatic Installation for centOS7

You can install the [requirements for the system](requirements-list.md) on centOS7 automatically by `localdb-tools/setting/db_server_install.sh`.<br>
The script can

- Check missing packages
- Install requirements for DAQ/DB Machine
- Enable MongoDB
- Confirme the installation status & Show quick tutorial

If you want to install on other platform, or install manually, see the [manual installation guide](manual-install.md).

## script

- Location: **localdb-tools/setting/db_server_install.sh**
- Syntax

```bash
$ cd localdb-tools/setting
$ ./db_server_install.sh
```

**This script will run commands which require administorative privilege.**<br>
**So the person who runs the script must be root or a sudoer.**

## Flow

```bash
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
