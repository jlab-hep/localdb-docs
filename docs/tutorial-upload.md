### Upload

You can scan and upload the test data into Local DB by `scanConsole -W`. <br>
First please confirm if the default config files are prepared, the commands are enabled, and the connection is established using `setup_db.sh`, <br>
and `scanConsole` use `${HOME}/.yarr/localdb/${HOSTNAME}_database.json`, `${HOME}/.yarr/localdb/user.json`, and `${HOME}/.yarr/localdb/${HOSTNAME}_site.json` as default config files.

```bash
$ ./localdb/setup_db.sh
<some texts>
[LDB] Checking the connection...
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# [Connection Test] DB Server: mongodb://127.0.0.1:27017/localdb
#DB INFO# ---> Connection is GOOD.
#DB INFO# -----------------------
<some texts>
$
$ ./bin/scanConsole \
-r configs/controller/emuCfg.json \
-c configs/connectivity/example_fei4b_setup.json \
-s configs/scans/fei4/std_digitalscan.json \
-W
<lots of text>
#DB INFO# -----------------------
#DB INFO# Function: Initialize
#DB INFO# Local DB Server: mongodb://127.0.0.1:27017
#DB INFO# ---> connection is good.
#DB INFO# -----------------------
#DB INFO# Uploading in the back ground. (log: ~/.yarr/localdb/log/)
```
> [Advanced tutorial for scanConsole -W](upload.md)

You can check if the upload is success in log file `${HOME}/.yarr/localdb/log/${day}.log`:

```log
2019-08-01 10:55:46,821 - INFO: -----------------------
2019-08-01 10:55:46,821 - INFO: Function: Upload Scan Data
2019-08-01 10:55:46,823 - INFO: Local DB Server: mongodb://127.0.0.1:27017
2019-08-01 10:55:46,826 - INFO: ---> connection is good.
2019-08-01 10:55:46,826 - INFO: Cache Directory: /home/akubata/work/YARR/data/000186_std_digitalscan/
2019-08-01 10:55:47,058 - INFO: Success
2019-08-01 10:55:47,060 - INFO: -----------------------
```
> [Advanced tutorial for another upload functions](upload.md)

### test
