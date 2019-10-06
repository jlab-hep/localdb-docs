# Check points

connectivity.json) <br>
![Connectivity config](https://github.com/jlab-hep/localDB-tools/blob/devel/docs/images/connectivity_config.png)

### 1. Module information
  **requirements**
  * serialNumber
  * componentType -> "Module"

  <details><summary>module document in connectivity.json (click)</summary><div>

  ```
  "module": {
      "serialNumber": "'module-serial-number'",
      "componentType": "Module"
  }
  ```
  ---
  </div></details>

### 2. Chip information
  **requirements**
  * chipType
  * config: path/to/chip config file
  * chipId -> must match the value "Parameter.ChipId" (written in chip config file) and "chipId" (written in component data registered in DB)
  * tx
  * rx

  <details><summary>chip document in connectivity.json (click)</summary><div>

  ```
  {
      "chipType": "RD53A",
      "chips": [
          {
              "serialNumber": "'module-serial-number'_chip1",
              "componentType": "Front-end Chip",
              "chipId": 1,
              "config": "configs/rd53a/'module-serial-number'/'module-serial-number'_chip1.json",
              "tx": 0,
              "rx": 0
          }
      ]
  }
  ```
  ---
  </div></details>

  <details><summary>chip document in component collection of DB (click)</summary><div>

  ```
  {
      "_id" : ObjectId("5cb720738b6de063fd546913"),
      "sys" : {
          "rev" : 0,
          "cts" : ISODate("2019-04-17T12:47:47.383Z"),
          "mts" : ISODate("2019-04-17T12:47:47.383Z")
      },
      "serialNumber" : "RD53A-002_chip1",
      "componentType" : "Front-end Chip",
      "chipType" : "RD53A",
      "chipId" : 0,
      "address" : "XX:XX:XX:XX:XX:XX",
      "user_id" : "5cb720618b6de0634a454262",
      "dbVersion" : 1
  }
  ```
  ---
  </div></details>