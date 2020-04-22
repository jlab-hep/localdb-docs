# Automatic Installation

**For macOS**, `localdb-tools/setting/macos/installer_macos.sh` can

- Check missing packages
- Install requirements for DAQ/DB Machine
- Enable MongoDB
- Confirme the installation status & Show quick tutorial

Check [Manual Installation](manual-install.md) to install requirements on other platform.

## scripts

- [installer_macos.sh](#installer_macossh)

### installer_macos.sh

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
