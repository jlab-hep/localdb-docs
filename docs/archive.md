# 1. Introduction

The **archive-tool** creates a/some archive tar.gz files to back-up Local DB.

# 2. Getting start

Please look at [Installation/Set-up Archive Tool](install.md) to set-up Archive Tool.

# 3. Usage

```bash
$ cd localdb-tools/sync-tool
$ ./bin/localdbtool-archive.sh -f my_archive_configure.yml
```

**Command Line Arguments**

* `-f|--config` : path to configure file.
* `-d|--data-path` : path to local data directory.
* `-a|--archive-path` : path to archives will be put.
* `-n|--n-archives` : # of archives to keep.
