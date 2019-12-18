# grafana

## Pre Confirmation

You should check if the grafana service is running on the machine as follows:

```bash
$ grafana-server -v
Version 6.5.2 (commit: 742d165, branch: HEAD)
```

If the service doesn't seem to be running,<br>
maybe the package has not been installed or the service has not been started, <br>
so please check [pre requirement page](requirements.md) to install/start the service.

## Upload influxDB

You should upload some dummy data into influxDB to check the Grafana.<br>
Please check [influxDB page](database_demonstration_influxdb.md) to upload data.

## Getting start

1. Access to [http://localhost:3000/](http://localhost:3000/) on the machine's browser where grafana was installed, and you can see the web page as follows:
![grafana top](images/demo_grafana_top.png)
2. Login with the username: 'admin' and the password: 'admin'
3. Add Database Sources
    - Click "Data Sources" in the Configuration in the side bar
    - Click "Add data source"
![grafana add db source](images/demo_grafana_db_source_1.png)
    - Set Name "dcsDB"
    - Set Type "influxDB"
    - Set URL "http://localhost:8086"
    - Set Database "dcsDB"
    - Click "Save & Test"
![grafana add db source config](images/demo_grafana_db_source_2.png)
4. Create New Dashboard
    - Click "Dashboard" in the Create in the site bar
    - Click "Add panel"
    - Click "Graph"
![grafana add dashboard](images/demo_grafana_dashboard_1.png)
    - Click "Panel Title" and click "Edit" from the list
    - Select "dcsDB" for Data Source
    - Click "Add Query" and Select the measurement channel (e.g. "dummy_thermal")
    - Select data value from the list (e.g. 3_temperature)
![grafana add dashboard](images/demo_grafana_dashboard_2.png)

Check [Grafana site](https://grafana.com/docs/grafana/latest/guides/getting_started/) for more detail.
