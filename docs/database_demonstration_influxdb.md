# influxDB

## Goal

Upload dummy DCS data into influxDB and Check the graph of DCS data using [grafana](database_demonstration_grafana.md)

## Pre Requirements

### influxDB

Just type 'influx' to check if the influxDB service is running.

```bash
$ influx
Connected to http://localhost:8086 version 1.7.9
InfluxDB shell version: 1.7.9
> exit
$
```

## Open port
```bash
$ firewall-cmd --zone=public --add-port=8086/tcp --permanent
$ firewall-cmd --reload
$ firewall-cmd --list-all
```


<!--
If the service doesn't seem to be running,<br>
maybe the package has not been installed or the service has not been started, <br>
so please check [pre requirement page](requirements.md) to install/start the service.

## Getting start

### 1. Clone Script

Some script to upload dummy data into influxDB is prepared in [the repository](https://gitlab.cern.ch/syamagay/influxdb_tools).

```bash
$ git clone https://gitlab.cern.ch/syamagay/influxdb_tools.git
$ cd influxdb_tools
$ git checkout devel
```

### 2. Run Script

```bash
$ ./dummydata.py
```

- Advanced (required 'istats' command)

```bash
$ ./shell.sh
```

### 3. Access to the Web Page

Access to [http://localhost:3000/](http://localhost:3000/) on the machine's browser where grafana was installed.<br>
Check [here](database_demonstration_grafana.md) to go to the steps for checking grafana service.

Finish!
-->

## More Detail

Check [influxDB site](https://docs.influxdata.com/influxdb/v1.7/introduction/getting-started/) for more detail.
