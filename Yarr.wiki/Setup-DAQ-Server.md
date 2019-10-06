This page describes how to setup Local DB system for YARR SW in DAQ Server

## Pre Requirements

- DAQ Server with [required libraries installed](https://github.com/jlab-hep/Yarr/wiki/Installation)

## Setup

* Setup tool: `YARR/localdb/setup_db.sh`

  <span style="color:red">__recommendation: non-sudo execution__</span>

  * Create config files
     * DB Config: ${HOME}/.yarr/localdb/database.json
     * Site Config: ${HOME}/.yarr/localdb/site.json
     * User Config: ${HOME}/.yarr/localdb/user.json
  * Check Python Modules and Install the missing ones (`~/.local/lib`)
  * Setup Local DB Tools for DAQ Server (`~/.local/bin`)
     * localdbtool-upload
     * localdbtool-retrieve
  
  ```bash   
  $ git clone https://gitlab.cern.ch/YARR/YARR.git
  $ checkout devel
  $ cd YARR/localdb
  $ ./setup_db.sh
  [LDB] Check the exist site config...NG!
  
  [LDB] Enter the institution name where this machine is, or 'exit' ... 
  # Answer here
  > Tokyo Institute of Technology
  
  [LDB] Confirmation
  	-----------------------
  	--  Mongo DB Server  --
  	-----------------------
  	IP address: 127.0.0.1
  	port: 27017
  	-----------------
  	--  Test Site  --
  	-----------------
      MAC address: XX.XX.XX.XX.XX.XX
      Machine Name: ${HOSTNAME}
  	Institution: Tokyo_Institute_of_Technology
  
  [LDB] Are you sure that is correct? [y/n]
  # Answer here and move on following process
  > y
  <lots of texts>
  This description is saved as path/to/YARR/localdb/README
  ```

  Check default database config files [here](https://github.com/jlab-hep/Yarr/wiki/database-config-file).
