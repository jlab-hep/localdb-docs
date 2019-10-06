This page describes how to setup Viewer Application in DB Server

## Pre Requirements

- DB Server with [required libraries installed](https://github.com/jlab-hep/Yarr/wiki/Installation)

## Setup

* Setup tool: `localDB-tools/setting/start_viewer.sh`

  <span style="color:red">__recommendation: non-sudo execution__</span>

  <span style="color:red">__This script should be run once for starting Viewer Application.__</span><br>
  <span style="color:red">__After the second run, the existing config could be overwritten.__</span>

  * create the config file

  ```bash
  $ git clone https://github.com/jlab-hep/localDB-tools.git
  $ cd localDB-tools/setting
  $ ./start_viewer.sh
  Local DB Server IP address: 127.0.0.1
  Local DB Server port: 27017
  Viewer Application Config: path/to/localDB-tools/viewer/conf.yml
 
  Are you sure that is correct? [y/n]
  > y
  # Answer here
  Done.
  $ python3 app.py --config path/to/localDB-tools/viewer/conf.yml &
  # -> Try accessing the DB viewer in your web browser
  #    From the DAQ machine: http://localhost:5000/localdb/
  #    From other machines : http://"HOST IP ADDRESS"/localdb/
  ```
  Additional options:<br>
  Set IP address of the Local DB Server
  - **-i ``<IP address>``** : Local DB server IP address, default: 127.0.0.1
  - **-p ``<port>``** : Local DB server port, default: 27017
  - **-c ``<config>``** : Viewer Application config file name, default: conf.yml

