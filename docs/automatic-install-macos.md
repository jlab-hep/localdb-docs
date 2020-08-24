# Automatic Installation for macOS

You can install the [requirements for the system](requirements-list.md) on macOS automatically by `localdb-tools/setting/macos/installer_macos.sh`.<br>
The script can

- Check missing packages
- Install requirements for DAQ/DB Machine
- Enable MongoDB
- Confirme the installation status & Show quick tutorial

If you want to install on other platform, or install manually, see the [manual installation guide](manual-install.md).

## script

- Location: **localdb-tools/setting/macos/installer_macos.sh**
- Syntax

```bash
$ cd localdb-tools/setting/macos
$ ./installer_macos.sh
```

**This script will run commands which require administorative privilege.**<br>
**So the person who runs the script must be root or a sudoer.**

## Flow

```zsh
$ cd localdb-tools/setting/macos
$ ./installer_macos.sh
[LDB] Looking for missing packages for Local DB and Tools ...
------------------------------------
          Missing packages
------------------------------------
 brew   : gnuplot
  .
  .
 python : arguments
  .
  .
------------------------------------
[LDB] Install these package? [y/n]
y

[LDB] Following steps will be done ...
[LDB] - Install required packages by brew & pip.
[LDB]
[LDB] You need to be root to perform this command.
[LDB] OK!

< Installing packages with many texts >

[LDB] Finished!!
[LDB]
[LDB] Final confirming ...
[LDB] Success!!
----------------------------------------
# Quick tutorial

< Simple instructions >

----------------------------------------
Enjoy!!
```
