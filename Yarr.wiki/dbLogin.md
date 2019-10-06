# Login Local DB system

You need to login Local DB system before the readout test to upload test data associated with the user information. <br>

`YARR/src/dbLogin.sh` can
* create the user config file: `${HOME}/.yarr/${DBUSER}_user.json`

In readout test, user/site data can be upload associated with test data by loading the user/site config file.

usage)
```
cd YARR/src
./dbLogin.sh [user account name]
```

## a) Login Database system / Create user config / Register user data

`dbLogin.sh` set the environment variable `DBUSER` to be [user account name]. <br>
You need to login Local DB once when you log in this machine. <br>
If there is not your user data in Local DB,
`dbLogin.sh` can 
* register your user data
* create the user config file `${HOME}/.yarr/${DBUSER}_user.json`

<details><summary>flow in the first registration (click)</summary><div>
<br>

![dbLogin flow user 1](https://github.com/jlab-hep/localDB-tools/blob/devel/docs/images/dbLogin_1.png)

</div></details>

<details><summary>flow from the second time (click)</summary><div>
<br>

![dbLogin flow user 2](https://github.com/jlab-hep/localDB-tools/blob/devel/docs/images/dbLogin_2.png)

</div></details>

<details><summary>user config file (click)</summary><div>
<br>

`${HOME}/.yarr/${DBUSER}_user.json`) <br>
![dbLogin flow user 2](https://github.com/jlab-hep/localDB-tools/blob/devel/docs/images/user_config.png)

</div></details>

## b) Create site config and Register site data

If there is not this site data in Local DB,
`dbLogin.sh` can 
* register the site data
* create the site config file `${HOME}/.yarr/address`

<details><summary>flow (click)</summary><div>
<br>

![dbLogin flow site](https://github.com/jlab-hep/localDB-tools/blob/devel/docs/images/dbLogin_3.png)

</div></details>

## c) Create database config

`dbLogin.sh` can 
* create database config file `${HOME}/.yarr/database.json` (overwrite if the file already exists.)

There are parameter lists in `database.json`
* stage list
  You can upload test data with the production stage name from this list. 
* environmental key list
  You can upload test data with DCS data from this list
* component list
  You can register component from this list

You can add items into the lists to register the items into Local DB,
but the items will be disabled in Viewer Application.

<details><summary>database config file (click)</summary><div>
<br>

`${HOME}/.yarr/database.json`) <br>
![database config](https://github.com/jlab-hep/localDB-tools/blob/devel/docs/images/database_config.png)

</div></details>