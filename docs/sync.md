# 1. Introduction

The **sync-tool** is to synchronize multiple Local DB servers for ITk.<br>
Before using sync-tool, we need a stable, network-accessible **master server** which handle whole ITK data.

![Sync overall](images/sync_overall.png)

# 2. Getting start

Please look at [Installation/Set-up Synchronization Tool](install.md) to set-up Synchronization Tool.

# 3. Usage

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
    - `auto` : will do `commit`, `fetch`, `pull` and `push` in order.
- `-f|--config` : path to configure file.
