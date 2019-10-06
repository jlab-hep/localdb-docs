
This page describes how to upload data into database by scanConsole in YARR.

![Scan and Upload](https://github.com/jlab-hep/localDB-tools/blob/devel/docs/images/scan_upload.png)

You can run the scan and upload the results into Local DB by following the steps (click the item to expand the description).

### Procedure

<details><summary> 0. Compile (click to expand) </summary><div>
<br>

Compile SW on `devel` branch to use YARR SW with Local DB system.

```
cd path/to/Yarr
cd src
git checkout devel
make -j4
```

***
</div></details>

<details><summary> 1. Login DB system (click to expand) </summary><div>
<br>

Login DB system by the script `YARR/src/dbLogin.sh` before the scan.

usage)
```shell-session
cd YARR/src
# set [account name] anything as you like.
source dbLogin.sh [account name] 
e.g.) source dbLogin.sh Arisa
```
> Required information
>* Account name (anything as you like)
>* Your name (FirstName LastName)
>* Your institution
>* Your identification key (if you want to set)
>* Location where you test
>* Machine's name
>
> user config file `[account name]_user.json` is created in ${HOME}/.yarr/

<details><summary>flow) (click)</summary><div>

![dbLogin flow user 1](https://github.com/jlab-hep/localDB-tools/blob/devel/docs/images/dbLogin_1.png)

</div></details>

***
</div></details>

<details><summary> 2. Create config files (click to expand) </summary><div>
<br>

Create [config files](https://github.com/jlab-hep/Yarr/wiki/config-files) and write component data into database by the script `YARR/src/configs/createConfig.sh`.

basic usage)
```
cd configs

./createConfig.sh \
-a [rd53a/fei4b] \
-m [serial number] \
-c [number of chips] \
-r [path/to/controller] \
-i [path/to/DCSconfig] \
-d

e.g.) 
./createConfig.sh \
-a rd53a \
-m ABC-001 \
-c 1 \
-r controller/specCfg.json \
-i testRunInfo.json \
-d
```
> config files are created in YARR/src/configs/[rd53a/fei4b]/[serial number]/
>* chip config files    copied from YARR/src/configs/defaults/default_[rd53a/fei4b].json
>* `connectivity.json`   
>* `controller.json`      copied from [path/to/controller]
>* `info.json`            copied from [path/to/DCSconfig]

<details><summary>flow) (click)</summary><div>

![Config Creation](https://github.com/jlab-hep/localDB-tools/blob/devel/docs/images/config_creation.png)

--> config files are created in YARR/src/configs/rd53a/ABC-001

</div></details>

***
</div></details>

<details><summary> 3-0. Confirmation (click to expand) </summary><div>
<br>

   Fix some values in config files as your setup.

  * [info.json](https://github.com/jlab-hep/Yarr/wiki/Test-information) <br>
    There are production information to upload additional information of the test.
    * production stage name (default: "Testing")
    * DCS (default: None)
  * [connectivity config](https://github.com/jlab-hep/Yarr/wiki/Connectivity) <br>
    There are component information. <br>
    DO NOT CHANGE SERIAL NUMBER.
    * Chip Id, config, tx/rx channel

***
</div></details>

<details><summary> 3-1. Scan (click to expand) </summary><div>
<br>

`YARR/src/doScan_[rd53a/fei4b].sh` can run the scan with uploading database

usage)
```
cd YARR/src
./doScan_[rd53a/fei4b].sh \
-m [serial number] \
-s [scan config] \
-d

e.g.)
./doScan_rd53a.sh \
-m ABC-001 \
-s configs/scans/rd53a/std_digitalscan.json \
-d
```
> This script can execute: <br>
> `./bin/scanConsole` <br>
> `-r configs/[rd53a/fei4b]/[serial number]/controller.json \` <br>
> `-c configs/[rd53a/fei4b]/[serial number]/connectivity.json \` <br>
> `-s [scan config] \` <br>
> `-p -W \` <br>
> `-I configs/[rd53a/fei4b]/[serial number]/info.json` <br>
> <br>
> scanConsole with option `-W` upload scan result into LocalDB

<details><summary>./bin/scanConsole) (click)</summary><div>

```shell-session
./bin/scanConsole \
-r [path to controller config] \
-c [path to connectivity config] \
-s [path to scan config] \
-p -W \
-I [path to environment info config]
 
e.g.) 
./bin/scanConsole \
-r configs/rd53a/ABC-001/controller.json \
-c configs/rd53a/ABC-001/connectivity.json \
-s configs/scans/rd53a/std_digitalscan.json \
-p -W \
-I configs/rd53a/ABC-001/info.json
``` 

***
</div></details>

You can check the results in '127.0.0.1:5000/localdb/' in browser if the viewer is running. <br>
(Ref. [About Viewer Application](https://github.com/jlab-hep/Yarr/wiki/Viewer))

***
</div></details>

<details><summary> 3-2. Register DCS (click to expand) </summary><div>
<br>

`YARR/src/bin/dbAccessor` can register DCS after scan.

usage)
```
./bin/dbAccessor -E data/last_scan/dcs_cache.json
```

There are `"status": "done"` in `data/last_scan/dcs_cache.json` if the registration is succeeded.

</div></details>

------

### More detail

* [About login Database system](https://github.com/jlab-hep/Yarr/wiki/dbLogin)

* [About config creation](https://github.com/jlab-hep/Yarr/wiki/config-files)

* [About scan with Local DB system](https://github.com/jlab-hep/Yarr/wiki/detailScan)
