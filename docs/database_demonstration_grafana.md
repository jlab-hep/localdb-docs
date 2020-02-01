# grafana

### Create ssh tunnel 
To see grafana on your browser, Do the bellow comand on your command prompt.<br>
**Change the server name according to the given name** (e.g.:root@localdbserver1)<br> 
Password is the DB server account's password.(Default is "password".)

```bash
$ ssh -2 -C -Y -L 3000:localhost:3000 root@localdbserverX -fN
Password:
```

## Getting start

### 1. Access to the Web Page

Access to [http://127.0.0.1:3000/](http://127.0.0.1:3000/) with the machine's browser on the same network as DB machine,<br>
and you can see the web page as follows:

![grafana top](images/demo_grafana_top.png)

### 2. Login

Login with the username: 'admin' and the password: 'admin'

### 3. Add Database Source

1. Click "Data Sources" in the Configuration in the side bar
2. Click "Add data source"

![grafana add db source](images/demo_grafana_db_source_1.png)

1. Set Name "dcsDB"
2. Set Type "influxDB"
3. Set URL "http://localhost:8086"
4. Set Database "dcsDB"
5. Click "Save & Test"

![grafana add db source config](images/demo_grafana_db_source_2.png)

### 4. Create New Dashboard
Skip this step and return here after run DCS controller.

1. Click "Dashboard" in the Create in the site bar
2. Click "Add panel"
3. Click "Graph"

![grafana add dashboard](images/demo_grafana_dashboard_1.png)

1. Click "Panel Title"
2. Click "Edit" from the list
3. Select "dcsDB" for Data Source
4. Click "Add Query" and Select the measurement channel (e.g. "Tempareture")
5. Select data value from the list (e.g. temp1)

![grafana add dashboard](images/demo_grafana_dashboard_2.png)

Finish installation. Back to the previous page and go to next step.
