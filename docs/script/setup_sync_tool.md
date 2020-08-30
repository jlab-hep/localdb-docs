# setup_sync_tool.sh

This is a script for setting the configuration of the [synchronization tool](../sync.md).<br>
This script creates the [synchronization tool config file](../config/sync.md), and you can run the [synchronization tool](../sync.md) with it.

- Location: `localdb-tools/sync-tool/setup_sync_tool.sh`
- Syntax:

```bash
$ cd localdb-tools/sync-tool
$ ./setup_sync_tool.sh
```


### Flow

1. Check/Create [localdb-tools/sync-tool/my_configure.yml](../config/sync.md)
2. Set the binary command in bin directory

### Usage

```bash
$ cd localdb-tools/sync_tool
$ ./setup_sync_tool.sh
[LDB] Welcome!
[LDB]
[LDB] Welcome to Local Database Tools!
[LDB] Check python modules...
[LDB] Requirements already satisfied
[LDB]
[LDB] Set editor command ... > vim
[LDB]
[LDB]
[LDB] Finish!
[LDB]
[LDB] Enable bash completion by ...
[LDB]   source /home/kubota/PhD/db/YARR/localdb-tools/sync-tool/src/share/bash-completion/completions/localdbtool-sync
[LDB]
[LDB] Start synchronization by ...
[LDB]   cd /home/kubota/PhD/db/YARR/localdb-tools/sync-tool
[LDB]   ./bin/localdbtool-sync.py --sync-opt <option> --config my_configure.yml
[LDB]
[LDB] More information: https://localdb-docs.readthedocs.io/en/master/
```
