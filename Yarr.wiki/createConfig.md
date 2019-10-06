**usage of createConfig.sh**

(basic use procedure)

<details><summary>flow)</summary><div>

![Config Creation](https://github.com/jlab-hep/localDB-tools/blob/devel/docs/images/config_creation.png)

---
</div></details>

```shell-session
$ cd Yarr/src/configs
$ ./createConfig.sh -a 'rd53a-or-fei4b' -m 'module-serial-number' -r 'path/to/controllerCfg' -i 'path/to/testInfoCfg' -c 'number of chips'
e.g.) 
$ ./createConfig.sh -a rd53a -m ABC-001 -r controller/specCfg.json -i testRunInfo.json -c 1
Created config directory rd53a/ABC-001
Created rd53a/ABC-001/controller.json     <--- copied from controller/specCfg.json
Created rd53a/ABC-001/info.json           <--- copied from testRunInfo.json
Created rd53a/ABC-001/connectivity.json
Create rd53a/ABC-001/ABC-001_chip1.json
---------------------
name: ABC-001_chip1
chipId: 1
---------------------
Change name ... [<chipName>/n] 
n
Change chipId ... [#(chipId)/n] 
0
Created ABC-001_chip1.json
```
---

<details><summary>to write component information into DB after config creation (click)</summary><div>

`./createConfig.sh -d` can write component information into database after config creation

```
$ cd Yarr/src/configs
$ ./createConfig.sh -a 'rd53a/fei4b' -m 'module-serial-number' -i 'path-to-userCfg' -c 'number of chips’ -d
e.g.) 
$ ./create_config.sh -a rd53a -m ABC-001 -r controller/specCfg.json -i testRunInfo.json -c 1 -d
Created config directory rd53a/ABC-001
Created rd53a/ABC-001/controller.json     <--- copied from controller/specCfg.json
Created rd53a/ABC-001/info.json           <--- copied from testRunInfo.json
Created rd53a/ABC-001/connectivity.json
Create rd53a/ABC-001/ABC-001_chip1.json
---------------------
name: ABC-001_chip1
chipId: 1
---------------------
Change name ... [<chipName>/n] 
n
Change chipId ... [#(chipId)/n] 
0
Created ABC-001_chip1.json
./bin/dbRegister -C configs/rd53a/ABC-001/connectivity.json 
Database: Register Component:
    connecitivity config file : configs/rd53a/ABC-001/connectivity.json
    Database: User Information 
    User name: <FirstName>_<LastName>
    Institution: <ABC_Laboratory>
    User identity: default
    Database: MAC Address: XX:XX:XX:XX:XX:XX
```
---
</div></details>

<details><summary>to reset config files based on the existing connectivity.json (click)</summary><div>

`./createConfig.sh` can reset chip config files based on existing connectivity.json and chip config files

```
$ cd Yarr/src/configs
$ ./createConfig.sh -a 'rd53a/fei4b' -m 'module-serial-number'
e.g.) ./create_config.sh -a rd53a -m ABC-001
Config files of ABC-001 are already exist, then move it to backup directory
( Created rd53a/ABC-001/info.json         <--- reset user config if you specify new one with '-i <new user config>' )
( Create rd53a/ABC-001/controller.json    <--- reset controller config if you specify new one with '-r <new controller config>' )
Reset ABC-001_chip1.json                  <--- chipId and name refers to existing chip config
```
---
</div></details>

<details><summary>to reset all config files (click)</summary><div>

`./createConfig.sh -R` can recreate config files (reset all config files and settings)

```
$ cd Yarr/src/configs
$ ./create_config.sh -a 'rd53a/fei4b' -m 'module-serial-number' -R
e.g.) ./create_config.sh -a rd53a -m ABC-001 -R
Reset config files of ABC-001
Move config files to backup directory before reset
Continue to remake config files ... [y/n]    <--- you can continue to create configs with "-i 'path-to-userCfg' -c 'number of chips’"
```
---
</div></details>