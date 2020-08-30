# setup_archive_tool.sh

This is a script for setting the configuration of the [archive tool](../tool/archive.md).<br>
This script creates the [archive tool config file](../config/archive.md), and you can run the [archive tool](../tool/archive.md) with it.

- Location: `localdb-tools/archive-tool/setup_archive_tool.sh`
- Syntax:

```bash
$ cd localdb-tools/archive-tool
$ ./setup_archive_tool.sh
```


### Flow

1. Check/Create [localdb-tools/archive-tool/my_archive_configure.yml](../config/archive.md)
2. Set the binary command in bin directory

### Usage

```bash
$ cd localdb-tools/archive-tool
$ ./setup_archive_tool.sh
[LDB] Welcome!
[LDB]
[LDB] Set editor command ... > vim
[LDB]
[LDB]
[LDB] Finish!
[LDB]
[LDB] Enable bash completion by ...
[LDB]   source /home/localdb-tools/archive-tool/src/share/bash-completion/completions/localdbtool-archive
[LDB]
[LDB] Start to archive by
[LDB]   cd /home/localdb-tools/archive-tool
[LDB]   ./bin/localdbtool-archive.sh -f my_archive_configure.yml
[LDB]
[LDB] More information: https://localdb-docs.readthedocs.io/en/master/
```
