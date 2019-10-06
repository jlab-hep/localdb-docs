`YARR/src/configs/createConfig.sh` can create config files and write component data into database.

usage)
```
cd YARR/src/configs

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

<details><summary>flow (click)</summary><div>

![Config Creation](https://github.com/jlab-hep/localDB-tools/blob/devel/docs/images/config_creation.png)

</div></details>

## structure

* YARR/src/configs
  * rd53a or fei4b
    * serial number
      * [serial number]_chip#.json : config file for chip
      * connectivity.json          : connectivity config file
      * controller.json            : controller config file (default is copied from specCfg.json)
      * info.json                  : test information config file
      * [backup]                   : backup directory

## config files

* [connectivity.json](https://github.com/jlab-hep/Yarr/wiki/Connectivity)
* controller.json : copied from `YARR/src/configs/controller/*.json`
* [serial number]\_chip#.json : copied from `configs/defaults/default_[asic].json` and changed chipId and name

  ```
  {
      "ASIC": {
          "Parameter": {
              "ChipId": #,
              "Name": "[serial number]_chip1"
          }
      }
  }
  ```
* [info.json](https://github.com/jlab-hep/Yarr/wiki/Test-information)

## Tools

### createConfig.sh

`YARR/src/config/createConfig.sh`

<details><summary>basic usage (click)</summary><div>

```shell-session
cd YARR/src/configs
./createConfig.sh \
-a [rd53a-or-fei4b] \
-m [module-serial-number] \
-c [number of chips] \
-r [path/to/controllerCfg] \
-i [path/to/testInfoCfg] 

e.g.) 
./createConfig.sh \
-a rd53a \
-m ABC-001 \
-c 1 \
-r controller/specCfg.json \
-i testRunInfo.json 

Create rd53a/ABC-001/ABC-001_chip1.json
---------------------
chip serial number: ABC-001_chip1
---------------------
Set chipId for chip1... [#(chipId)] 
0

serial number: ABC-001
controller config: controller/specCfg.json
dcs config: testRunInfo.json
num of chips: 1
** ABC-001_chip1
    chip serial number: ABC-001_chip1
    chipId: 0

Make sure? [y/n]
y
Created config directory rd53a/ABC-001
Created rd53a/ABC-001/controller.json     <--- copied from controller/specCfg.json
Created rd53a/ABC-001/info.json           <--- copied from testRunInfo.json
Created rd53a/ABC-001/connectivity.json
Created ABC-001_chip1.json
```
---

</div></details>

<details><summary>component registration (click)</summary><div>

`./createConfig.sh` with option `-d` can register component data after config creation

```
cd YARR/src/configs
./createConfig.sh \
-a [rd53a-or-fei4b] \
-m [module-serial-number] \
-c [number of chips] \
-r [path/to/controllerCfg] \
-i [path/to/testInfoCfg] \
-d

e.g.) 
./createConfig.sh \
-a rd53a \
-m ABC-001 \
-c 1 \
-r controller/specCfg.json \
-i testRunInfo.json 

Create rd53a/ABC-001/ABC-001_chip1.json
---------------------
chip serial number: ABC-001_chip1
---------------------
Set chipId for chip1... [#(chipId)] 
0

serial number: ABC-001
controller config: controller/specCfg.json
dcs config: testRunInfo.json
num of chips: 1
** ABC-001_chip1
    chip serial number: ABC-001_chip1
    chipId: 0

Make sure? [y/n]
y
Created config directory rd53a/ABC-001
Created rd53a/ABC-001/controller.json     <--- copied from controller/specCfg.json
Created rd53a/ABC-001/info.json           <--- copied from testRunInfo.json
Created rd53a/ABC-001/connectivity.json
Created ABC-001_chip1.json

./bin/dbRegister -C configs/rd53a/ABC-001/connectivity.json 
DBHandler: Register Component:
    connecitivity config file : configs/rd53a/ABC-001/connectivity.json
DBHandler: User Information 
    User name: [FirstName]_[LastName]
    Institution: [ABC_Laboratory]
    User identity: default
DBHandler: MAC Address: XX:XX:XX:XX:XX:XX
```
---
</div></details>

<details><summary>Reset config files based on the existing connectivity.json (click)</summary><div>

`./createConfig.sh` can reset chip config files based on existing connectivity.json and chip config files

```
cd YARR/src/configs
./createConfig.sh \
-a [rd53a/fei4b] \
-m [module-serial-number]

e.g.) 
./create_config.sh \
-a rd53a \
-m ABC-001
Config files of ABC-001 are already exist, then move it to backup directory
( Created rd53a/ABC-001/info.json         <--- reset user config if you specify new one with '-i [new user config]' )
( Create rd53a/ABC-001/controller.json    <--- reset controller config if you specify new one with '-r [new controller config]' )
Reset ABC-001_chip1.json                  <--- chipId and name refers to existing chip config
```
---
</div></details>

<details><summary>Reset all config files (click)</summary><div>

`./createConfig.sh -R` can recreate config files (reset all config files and settings)

```
cd YARR/src/configs
./create_config.sh \
-a [rd53a/fei4b] \
-m [module-serial-number] \
-R

e.g.) 
./create_config.sh \
-a rd53a \
-m ABC-001 \
-R
Reset config files of ABC-001
Move config files to backup directory before reset
Continue to remake config files ... [y/n]    
    # you can continue to create configs with "-i [new user config] -c [number of chips]"
```
---
</div></details>