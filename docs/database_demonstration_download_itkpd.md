# Module Download from ITkPD

### Create ssh tunnel 
To see LocalDB viewer on your browser, Do the bellow comand on your command prompt.<br>
**Change the server name according to the given name** (e.g.:root@localdbserver1)<br> 
Password is the DB server account's password.(Default is "password".)

```bash
$ ssh -2 -C -Y -L 5000:localhost:5000 root@localdbserverX -fN
Password:
```

Download the component data from ITkPD.<br>
Go to the downloading page [http://127.0.0.1:5000/localdb/download_component](http://127.0.0.1:5000/localdb/download_component)

**a more instruction here**

![download from itkpd](images/download_component_from_itkpd.png)

You can check the downloaded component data using Viewer Application.<br>
Check [http://127.0.0.1:5000/localdb/components](http://127.0.0.1:5000/localdb/components) on the machine's browser where app.py is running,<br>
and there are the module data whose serial number is ATLAS serial number.

Finish. Back to the previous page and go to next step.
