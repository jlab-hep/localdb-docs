Prepare the environmental dat file or json file to upload DCS data in scan into DB.

## 1. Environmental Data File
Prepare the environmental dat/csv file written in this format.

![DCS data](https://github.com/jlab-hep/localDB-tools/blob/devel/docs/images/dcs_file.png)
>* lines
>   * 1st line: key null key1 key2 key3 ... 
>   * 2nd line: num null num1 num2 num3 ... 
>   * 3rd line: mode null mod1 mod2 mod3 ... 
>   * 4th line: setting null set1 set2 set3 ...
>   * 5th line: string unixtime val1 val2 val3 ...
>
>* format
>   * key# and mod# are string <br>
>   * num# and unixtime are integral number <br>
>   * set# and val# are float number <br>
>   * values are separated by commas in csv file, and by en space in dat file 

## 2. Environmental Config File

Set path to dat file for the DCS key in json file `YARR/src/configs/[fei4b/rd53a]/[serial number]/info.json`.

<details><summary>info.json (click)</summary><div>

![DCS config](https://github.com/jlab-hep/localDB-tools/blob/devel/docs/images/dcs_config.png)
>* key is selected from the list in the database config file `${HOME}/.yarr/database.json`
>* upload DCS data from data file in the path if the status is "enabled"
>* key and num specify the values in data file
>* description distinguish data with the same key
>* value is DCS value set manually instead of setting path to data file

</div></details>

## 2. Register DCS 

```
cd YARR/src
./doScan_[fei4b/rd53a].sh -m [serial number] -s [scan config] -d
~~~ scan ~~~
./bin/dbAccessor -E data/last_scan/dcs_cache.json
```

DCS data while scanning will be uploaded into Local DB.