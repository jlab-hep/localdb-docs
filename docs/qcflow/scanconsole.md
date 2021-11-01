Previous step.<br>
[Upload QC test results into LocalDB](nonelectricalwire.md)<br>

# QC scan

## Retrieve scan config files
Before taking scan result, we need to retrieve module info from LocalDB and create scan config file(e.g. connectivity.json).



## scanConsole and upload scan results

Run the scan using the following command.(e.g. digitalscan)<br>
The scan result is automatically stored when you put "-W" option.
```bash
$ ./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/std_digitalscan.json -W
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

Check the test results [http://127.0.0.1:5000/localdb/scan](http://127.0.0.1:5000/localdb/scan).<br>


We are also developing the script to run these scan at once.<br>
Scan Operator repo ([https://gitlab.cern.ch/YARR/utilities/scan-operator](https://gitlab.cern.ch/YARR/utilities/scan-operator))

After uploading scans results for Full Electrical Test, select scans and register as a QC-test result.

Go to next step.<br>
[Select Scans test results](upload_resultwire.md)<br>
