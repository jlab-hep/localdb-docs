## Pre Requirements

There are several softwares required for Local DB:

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
$ git clone https://gitlab.cern.ch/YARR/YARR.git
$ cd YARR
$ git checkout devel

# 1-2. Local DB Tools
$ git clone https://gitlab.cern.ch/YARR/localdb-tools.git
$ cd localdb-tools
$ git checkout devel
```

You can install them on **centOS7** automatically or manually:

- [Automatic Installation](automatic-install.md)
- [Manual Installation](manual-install.md)
