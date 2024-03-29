# Create ssh tunnels from the DAQ machine to the DB machine

## What is "ssh tunnel"?

![ssh tunnel](../images/qc-flow/ssh_tunnel.png)

## Create ssh tunnels
In order to connect to the DBs and the web applications(mongoDB, influxDB, LocalDB viewer, grafana) in the DB machine from your local machine, Run the following comand on your shell.<br>
**Change the server name accordingly** (e.g.:parrot@localdbserver99)<br>
Password is the DB server account's password.

```bash
# For mongoDB
$ ssh -L 27017:localhost:27017 parrot@localdbserverXX -fN -p22
Password:
# For influxDB
$ ssh -L 8086:localhost:8086 parrot@localdbserverXX -fN
Password:
# For LocalDB viewer
$ ssh -L 5000:localhost:5000 parrot@localdbserverXX -fN
Password:
# For grafana
$ ssh -L 3000:localhost:3000 parrot@localdbserverXX -fN
Password:
```
![Create ssh tunnel](../images/qc-flow/sshtunnel_to_remote.png)
Go to next step.<br>
[Download module ID infos](download_itkpd.md)<br>
