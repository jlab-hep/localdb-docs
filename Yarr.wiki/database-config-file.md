  Default config files for Local DB will be created in `${HOME}/.yarr/localdb/etc`
  
  <details><summary>database.json</summary><div>

  ```json
  {
      "hostIp": "127.0.0.1",
      "hostPort": "27017",
      "dbName": "localdb",
      "stage": [
          "Bare Module",
          "Wire Bonded",
          "Potted",
          "Final Electrical",
          "Complete",
          "Loaded",
          "Parylene",
          "Initial Electrical",
          "Thermal Cycling",
          "Flex + Bare Module Attachment",
          "Testing"
      ],
      "environment": [
          "vddd_voltage",
          "vddd_current",
          "vdda_voltage",
          "vdda_current",
          "hv_voltage",
          "hv_current",
          "temperature"
      ],
      "component": [
          "Front-end Chip",
          "Front-end Chips Wafer",
          "Hybrid",
          "Module",
          "Sensor Tile",
          "Sensor Wafer"
      ]
  }
  ```
  - hostIp : ip address of DB server (default: 127.0.0.1)
  - port : port number where Local DB is running (default: 27017)
  - dbName : database name (default: "localdb")
  - stage : the list of the stages for Module Production
  - environment : the list of the DCS keywords for DCS data
  - component : the list of the components for registration of the Module
  
  </div></details> 

  <details><summary>site.json</summary><div>

  ```json
  {
      "macAddress": "XX.XX.XX.XX.XX.XX",
      "hostname": "HOSTNAME",
      "institution": "ABC_Laboratory"
  }
  ```
  - macAddress : MAC address of the DAQ machine 
  - hostname : host name of the DAQ machine
  - institution : where the DAQ machine is

  </div></details>

  <details><summary>user.json</summary><div>

  ```json
  {
      "userName": "${USER}",
      "institution": "${HOSTNAME}",
      "description": "default"
  }
  ```
  - userName : user's name (default: $USER)
  - institution : user's institution (default: $HOSTNAME)
  - description : user's description (default: "default")

  </div></details>