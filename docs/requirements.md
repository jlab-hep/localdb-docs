## Pre Requirements

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
# 0. Check git command
# Check & Install git command
$ which git > /dev/null 2>&1; if [ $? = 1 ]; then sudo yum install git; fi

# 1-1. YARR SW
## Some Local DB functions are not available yet in YARR v1.1.0.
## Please change to devel branch if want to use.
$ git clone https://gitlab.cern.ch/YARR/YARR.git
$ cd YARR

# 1-2. Local DB Tools
$ git clone https://gitlab.cern.ch/YARR/localdb-tools.git
$ cd localdb-tools
```

You can install them automatically or manually:

- [Automatic Installation (centOS7)](automatic-install.md)
- [Manual Installation (centOS7)](manual-install.md)
- [Manual Installation (macOS)](manual-install-macos.md)
