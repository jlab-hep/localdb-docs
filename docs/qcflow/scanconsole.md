Previous step.<br>
[Upload QC test results into LocalDB](nonelectricalwire.md)<br>

# QC scan

## Retrieve scan config files
Before taking scan result, we need to retrieve module info from LocalDB and create scan config file(e.g. connectivity.json). We will use `dbAccesser` to pull config files for this tutorial.

First, we will create a connectivity file:
```bash
$ cd /PATH/TO/YARR
$ ./bin/dbAccessor -D -n <Module SN>
[18:49:14:304][  info  ][  dbAccessor   ]: DBHandler: Retrieve Config Files
[18:49:15:621][  info  ][   Local DB    ]: -----------------------
[18:49:15:624][  info  ][   Local DB    ]: Checking connection to DB Server: mongodb://127.0.0.1:27017/localdb ...
[18:49:15:637][  info  ][   Local DB    ]: ---> Good connection!
[18:49:15:663][  info  ][   Local DB    ]: Retrieve/Create data files in ./db-data
[18:49:15:663][warning ][   Local DB    ]: Already exist directory: ./db-data.

Override it? [y/n] (Exit without doing anything if "n")
> y
[18:49:18:340][  info  ][   Local DB    ]: component data ID: 61824d5c0a9e0e000a0f71b8
[18:49:18:340][  info  ][   Local DB    ]: - Parent    : 20UPGXM0100000 (module)
[18:49:18:340][  info  ][   Local DB    ]: - Chip Type : RD53A
[18:49:18:341][  info  ][   Local DB    ]: - Chips     : 20UPGXF0000000
[18:49:18:341][  info  ][   Local DB    ]: - Stage     : MODULEWIREBONDING
[18:49:18:341][  info  ][   Local DB    ]: Retrieve ... ./db-data/connectivity.json
[18:49:18:345][warning ][   Local DB    ]: Please confirm if there is no mistake in "./db-data/connectivity" before running scanConsole.
[18:49:18:345][warning ][   Local DB    ]: And create chip config files by:
[18:49:18:345][warning ][   Local DB    ]:     ./bin/createConfig -t RD53A -n 20UPGXF0000000 -o ./db-data/20UPGXF0000000.json
[18:49:18:345][  info  ][   Local DB    ]: -----------------------
```
Then, we will create a chip config file:

```bash
$ ./bin/createConfig -t RD53A -n 20UPGXF0000000 -o ./db-data/20UPGXF0000000.json
[18:52:29:903][  info  ][  cfgCreator   ]: Starting config creator!
[18:52:29:904][  info  ][  cfgCreator   ]: Parsing command line parameters ...
[18:52:29:904][  info  ][  cfgCreator   ]: Chip Type  : RD53A
[18:52:29:904][  info  ][  cfgCreator   ]: Chip Name  : 20UPGXF0000000
[18:52:29:904][  info  ][  cfgCreator   ]: Ouput file : ./db-data/20UPGXF0000000.json
[18:52:30:116][  info  ][  cfgCreator   ]: Writing default config to file ...
[18:52:30:219][  info  ][  cfgCreator   ]: ... done! Success, bye!
```
!!! Warning
    `ChipId` written in chip config file become `0`. Please fix line 178 of chip file to `"ChipId": 1` <br>

You can see scan config files in `/Yarr/db-data`:

```json
e.g.: connectivity.json
{
   "stage": "MODULEWIREBONDING",
   "chips": [
       {
           "name": "20UPGXF0000000",
           "config": "./db-data/20UPGXF0000000.json",
           "chipId": 1,
           "tx": 0,
           "rx": 0
       }
   ],
   "module": {
       "serialNumber": "20UPGXM0100000",
       "componentType": "module"
   },
   "chipType": "RD53A"

}
```

We can start to upload scan results to LocalDB!

## scanConsole and upload scan results

Run the scan using the following command.(e.g. digitalscan)<br>
The scan result is automatically stored when you put "-W" option.
```bash
$ ./bin/scanConsole -r configs/controller/emuCfg_rd53a.json -c db-data/connectivity.json -s configs/scans/rd53a/std_digitalscan.json -W
```

Scan items required for Full Electrical Test(Pixel Failure Test) are bellow:<br>
- std_analogscan<br>
- std_digitalscan<br>
- std_thresholdscan<br>
- std_totscan<br>
- std_noisescan<br>
- std_crosstalkscan<br>

On the `real module` QC, we need to do a tuning routine: [Electrical testing doc.](https://cds.cern.ch/record/2723333/files/ATL-COM-ITK-2020-020.pdf)

For this tutorial, we will skip a tuning routine to take scans results quickly.  We take scan results with following commands:


```bash
$ ./bin/scanConsole -r configs/controller/emuCfg_rd53a.json -c db-data/connectivity.json -s configs/scans/rd53a/std_digitalscan.json -W
$ ./bin/scanConsole -r configs/controller/emuCfg_rd53a.json -c db-data/connectivity.json -s configs/scans/rd53a/std_analogscan.json -W
$ ./bin/scanConsole -r configs/controller/emuCfg_rd53a.json -c db-data/connectivity.json -s configs/scans/rd53a/std_thresholdscan.json -W
$ ./bin/scanConsole -r configs/controller/emuCfg_rd53a.json -c db-data/connectivity.json -s configs/scans/rd53a/std_totscan.json -t 10000 -W
$ ./bin/scanConsole -r configs/controller/emuCfg_rd53a.json -c db-data/connectivity.json -s configs/scans/rd53a/std_noisescan.json -W
$ ./bin/scanConsole -r configs/controller/emuCfg_rd53a.json -c db-data/connectivity.json -s configs/scans/rd53a/std_crostalkscan.json -W
```

Check the test results [http://127.0.0.1:5000/localdb/scan](http://127.0.0.1:5000/localdb/scan) or http://IPADRESS:5000/localdb/scan.<br>


We are also developing a SW to run these scan at once.<br>
Scan Operator repo ([https://gitlab.cern.ch/YARR/utilities/scan-operator](https://gitlab.cern.ch/YARR/utilities/scan-operator))

After uploading scans results for Full Electrical Test, select scans and register as a QC-test result.

Go to next step.<br>
[Select Scans test results](upload_resultwire.md)<br>
