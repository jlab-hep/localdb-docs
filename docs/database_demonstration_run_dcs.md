# Run DCS controller and Checking in Grafana

## Create ssh tunnel
```bash
$ ssh -2 -C -Y -L 8086:localhost:8086 root@localdbserverX -fN 
Password:
```

## Run temperature controller

```bash
$ cd ~/work/E4control/e4control
$ python3 temp_controller.py
This measurement runs until ctrl+C is pressed!
Temp1:??.??C     Temp2:??.??C
...
```

## Run temperature controller
```bash
$ cd ~/work/E4control/e4control
$ python3 LV_controller.py
This measurement runs until ctrl+C is pressed!
TTI2:
...
```

