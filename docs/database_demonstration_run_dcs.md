# Hook up module to devices and Run DCS controller

## Hook up module to devices
in edit

## Create ssh tunnel 
To connect influxDB of DB machine from your local machine, Do the bellow comand on your command prompt.<br>
**Change the server name according to the given name** (e.g.:root@localdbserver1)<br> 
Password is the DB server account's password.(Default is "password".)

```bash
$ ssh -L 8086:localhost:8086 root@localdbserverX -fN 
Password:
```
![ssh tunnel influxdb](images/sshtunnel_influxdb.png)

## (1)Run script to get temperature
To get environmental temperature and store the data into influxDB, do the following command.<br>
<span style="color: red; ">**Don't stop this process through readout. Chenge the screen from next step.**</span>

```bash
$ cd ~/work/E4control/e4control
$ python3 temp_controller.py
This measurement runs until ctrl+C is pressed!
Temp1:??.??C     Temp2:??.??C
...
```

## (2)Run LV IV
in edit


## (3)Run LV PS controller
To turn on the LV PS and get the current and voltage, do the following command.<br>
<span style="color: red; ">**Don't stop this process through readout. Chenge the screen from next step.**</span>
```bash
$ cd ~/work/E4control/e4control
$ python3 LV_controller.py
This measurement runs until ctrl+C is pressed!
TTI2:
...
```

![DCS system](images/demo_dcs_system.png)

