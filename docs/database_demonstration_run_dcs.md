# Run DCS controller and Checking in Grafana

## Create ssh tunnel
```bash
$ ssh -2 -C -Y -L 8086:localhost:8086 {DB server IP} -fN
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

## Checking data on grafana
You can see the data on grafana.
Go to step4 og this page.[here](database_demonstration_grafana.md)


