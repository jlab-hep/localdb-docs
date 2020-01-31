# Run DCS controller and Checking in Grafana

## Create ssh tunnel
```bash
$ ssh -2 -C -Y -L 8086:localhost:8086 root@localdbserverX -fN 
Password:
$ 
```

## Run temperature controller

```bash
$ cd ~/work/E4control/e4control
$ python3 temp_controller.py

```

## Run temperature controller
```bash
$ cd ~/work/E4control/e4control
$ python3 LV_controller.py

```

