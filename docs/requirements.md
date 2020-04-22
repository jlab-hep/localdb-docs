## Pre Requirements & Installation

There are several requirements for Local DB:

- Supported OS
    - centOS7
    - macOS greater than 10.14
- [Requirements List](requirements-list.md)
    - yum packages
    - python packages
    - Mongo DB
- git repository

```bash
# for centos
# 0. Check git command
# Check & Install git command
$ which git > /dev/null 2>&1; if [ $? = 1 ]; then sudo yum install git; fi
```

- YARR SW
```bash
## Some Local DB functions are not available yet in YARR v1.1.0.
## Please change to devel branch if want to use.
$ cd <YOUR_WORK DIRECTRY>
$ git clone https://gitlab.cern.ch/YARR/YARR.git
```

- Local DB Tools
<br>It is better to put this SW on the same level as YARR-SW.
```bash
$ cd <YOUR_WORK DIRECTRY>
$ git clone https://gitlab.cern.ch/YARR/localdb-tools.git
```

You can install them automatically or manually:

- [Automatic Installation (centOS7)](automatic-install.md)
- [Automatic Installation (macOS)](automatic-install-macos.md)
- [Manual Installation (centOS7)](manual-install.md)
- [Manual Installation (macOS)](manual-install-macos.md)
