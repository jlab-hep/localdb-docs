# info.json

Make it to suit test environment. (ref. `Yarr/src/configs/testRunInfo.json`)

![DCS config](https://github.com/jlab-hep/localDB-tools/blob/devel/docs/images/dcs_config.png)
>* assembly
>   * stage: production stage of the test 
>* environments
>   * key: keyword of the environmental item
>   * num: the order of environmental keyword
>   * description: description + unit of the environmental keyword
>   * path/value: path to the environmental dat file, or the environmental data by setting manually
>   * status: enabled/disabled to register DCS data
>   * margin(option): time margin[s] 

## assembly
* stage 

  The assembly stage of this module. <br>
  Put the keyword from the list: 

  <details><summary>${HOME}/.yarr/database.json</summary><div>

  ```
  {
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
          "Flex + Bare Module Attachment"
      ]
  }
  ```
  ---
  </div></details>

## environments 
* key

  The environmental key the user wants to upload the data in scanning into DB. <br>
  Put the keyword from the list:

  <details><summary>${HOME}/.yarr/database.json</summary><div>

  ```
  {
      "environment": [
          "vddd_voltage",
          "vddd_current",
          "vdda_voltage",
          "vdda_current",
          "hv_voltage",
          "hv_current",
          "temperature"
      ],
  } 
  ```

  ---
  </div></details>

* status
  
  Set "enabled" to upload the environmental data.

* path or value

  It is possible to upload the environmental data written in [the fixed format](https://github.com/jlab-hep/Yarr/wiki/DCS-information) by setting { "path": path/to/data }. <br>
  It is also possible to upload only the data by setting { "value": ### }.
  
* description and num

  The description including the unit. <br>
  If there are same key but different data, separate them with different description/num.