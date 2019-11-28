# Synchronization Tool

The **Synchronization Tool** synchronizes multiple Local DB servers for ITk.<br>
Before using sync-tool, we need a stable, network-accessible **master server** which handle whole ITK data.

![Sync overall](images/sync_overall.png)

Contents:

1. [Command](#1-command)
2. [Getting Start](#2-getting-start)
3. [Usage](#3-usage)
4. [FAQ](#4-faq)

## 1. Command

**localdb-tools/sync-tool/localdbtool-sync.py**

```bash
$ ./bin/localdbtool-sync.py --sync-opt <option> --config my_configure.yml
```

## 2. Getting start

Please check [Pre Requirements](requirements.md) to install required packages.<br>
And please be sure to setup Synchronization Tool setting using `localdb-tools/sync-tool/setup_sync_tool.sh`. <br>
This script performs

- to confirm the config file ( [localdb-tools/sync-tool/my_configure.yml](config.md) )
- to set the binary command in bin directory

```bash
$ cd localdb-tools/sync-tool
$ ./setup_sync_tool.sh
< Setting up with some texts >
```

## 3. Usage

```bash
$ cd localdb-tools/sync-tool
$ ./bin/localdbtool-sync.py  --sync-opt commit --config my_configure.yml
```

**Command Line Arguments**

- `--sync-opt` : options for sync-tool
    - `commit` : commit all new/modified data which taken on the local.
    - `push` : upload committed data to the master server.
    - `fetch` : get commits from the master server.
    - `pull` : get committed data from the master server.
- `-f|--config` : path to configure file.

### a. Pull Data from Master Server

1. commit
2. fetch
3. pull

### b. Push Data to Master Server

1. commit
2. fetch
3. (pull)
4. push

## 4. FAQ

in edit.
