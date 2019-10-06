After step 0 and 1 in [Quick tutorial](https://github.com/jlab-hep/Yarr/wiki/Quick-tutorial).

## 2) Ready

It will read module and chip serial # from connectivity. So, it is necessary to add these to connectivity you will use.

For example, in case of using one RD53A single chip card, create a connectivity config json and add `"serialNumber": "0x7777"`. It looks like below (e.g. Yarr/src/config/connectivity/rd53a_setup.json)
```
{
    "chipType" : "RD53A",
    "chips" : [
        {
            "serialNumber": "0x7777",
            "config" : "configs/rd53a_test.json",
            "tx" : 0,
            "rx" : 0
        }
    ]
}
```

## 3) Use 'scanConsole'

Execute 'Yarr/src/tools/scanConsole.cpp' with option "-W " and "-I "

e.g.) 
```
/bin/scanConsole -r configs/controller/specCfg.json -p \
-c configs/connectivity/rd53a_setup.json \
-s configs/scans/rd53a/std_analogscan.json \
-W \
-I configs/testRunInfo.json
```

* It will create component document of module/chips if there is no their in database.
* It will write all output files on scanConsole output directory to database.
* For multi chips module, it will find and pick each chip's file by chip's name. So, do not change the chips' name during scan.
