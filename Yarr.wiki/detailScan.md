
<details><summary>Scan procedure (click)</summary><div>

```shell-session
./bin/scanConsole \
-r [controller config] \
-c [connectivity config] \
-s [scan config] \
-p -W \
-I [environment info]

e.g.) 
./bin/scanConsole \
-r configs/rd53a/ABC-001/controller.json \
-c configs/rd53a/ABC-001/connectivity.json \
-s configs/scans/rd53a/std_digitalscan.json \
-p -W \
-I configs/rd53a/ABC-001/info.json
``` 
---
</div></details>

You can check the results in '127.0.0.1:5000/localdb/' in browser if the viewer is running.

## 4) Useful scripts

<details><summary> Yarr/src/doScan_rd53a.sh (click)</summary><div>

`doScan_rd53a.sh` can run a single scan for rd53a.

```
$ ./doScan_rd53a.sh -m 'module-serial-number' -s 'scan-type' [-r ControllerCfg] [-n ConnectivityCfg] [-i EnvironmentCfg] [-c TargetCharge] [-t TargetTot] [-p TargetPreamp] [-M mask] [-d #upload into DB] [-l #save log file]
```

For example after creating config file with `createConfig.sh`,
```
$ cd Yarr/src
$ ./doScan_rd53a.sh -m ABC-001 -s std_digitalscan    # not upload into database
---> this can run: ./bin/scanConsole -r configs/rd53a/ABC-001/controller.json -c configs/rd53a/ABC-001/connectivity.json -s configs/scans/rd53a/std_digitalscan.json -p -m -1
$ ./doScan_rd53a.sh -m ABC-001 -s std_digitalscan -d # upload into database
---> this can run: ./bin/scanConsole -r configs/rd53a/ABC-001/controller.json -c configs/rd53a/ABC-001/connectivity.json -s
```
---
</div></details>

<details><summary> Yarr/src/doScan_fei4b.sh (click)</summary><div>

`doScan_fei4b.sh` can run a single scan for fei4b.

```
$ ./doScan_fei4b.sh -m 'module-serial-number' -s 'scan-type' [-r ControllerCfg] [-n ConnectivityCfg] [-i EnvironmentCfg] [-c TargetCharge] [-t TargetTot] [-p TargetPreamp] [-M mask] [-d #upload into DB] [-l #save log file]
```
 
For example after creating config file with `createConfig.sh`,
```
$ cd Yarr/src
$ ./doScan_fei4b.sh -m KEK-777 -s digitalscan    # not upload into database
---> this can run: ./bin/scanConsole -r configs/fei4b/KEK-777/controller.json -c configs/fei4b/KEK-777/connectivity.json -s digitalscan -p -m -1
$ ./doScan_fei4b.sh -m KEK-777 -s digitalscan -d # upload into database
---> this can run: ./bin/scanConsole -r configs/fei4b/KEK-777/controller.json -c configs/fei4b/KEK-777/connectivity.json -s digitalscan -p -m -1 -W -I configs/fei4b/KEK-777/info.json
```
---
</div></details>

<details><summary> Yarr/src/doEverything.sh (click)</summary><div>

`doEverything.sh` can run all scans. (QA)

```
$ ./doEverything.sh -a rd53a -m 'module-serial-number'    # not upload into database
$ ./doEverything.sh -a rd53a -m 'module-serial-number' -d # upload into database
```

For example,
```
$ cd Yarr/src
$ ./doEverything.sh -a rd53a -m ABC-001 -d
```
---
</div></details>