# Connectivity Config

You can specify the configuration of the component data when executing the scan and uploading data into Local DB.

#### File Format

The connectivity configuration file uses the JSON format.

##### SCC

```json
{
    "chipType" : "RD53A",
    "chips" : [
        {
            "config" : "configs/RD53A-001.json",
            "tx" : 0,
            "rx" : 0
        }
    ]
}
```

##### Quad

```json
{
    "module": {
        "serialNumber": "RD53A-Quad"
    },
    "chipType" : "RD53A",
    "chips" : [
        {
            "config" : "configs/RD53A-001.json",
            "tx" : 0,
            "rx" : 0
        },
        {
            "config" : "configs/RD53A-002.json",
            "tx" : 0,
            "rx" : 1
        },
        {
            "config" : "configs/RD53A-003.json",
            "tx" : 0,
            "rx" : 2
        },
        {
            "config" : "configs/RD53A-004.json",
            "tx" : 0,
            "rx" : 3
        }
    ]
}
```
#### Options

##### Core Options

- `chipType`<br>
_Type_ : string<br>
Specifies the chip type (e.g. FEI4B, RD53A)

- `chips`<br>
_Type_ : list<br>
Specifies the chips to test and upload.<br>
You can upload scan results linked to the chip data with the name written in the [chip config file](chip.md) specified by the "config".
    - `config`<br>
      _Type_ : string<br>
      Specifies the path to [chip config file](chip.md)
    - `tx`<br>
      _Type_ : int<br>
      Specifies the TX channel.
    - `rx`<br>
      _Type_ : int<br>
      Specifies the RX chennel.

##### Addtional Options

- `module`<br>
_Type_ : dictionary<br>
Specifies the module to test and upload.<br>
If the module component data is registered in the Local DB, you can upload scan results linked to the module data as well.<br>
If not, the scan results will only be linked to the chip data.
    - `serialNumber`<br>
      _Type_ : string<br>
      Specifies the serial number of the module component.<br>
    - `componentType`<br>
      _Type_ : string<br>
      If you register the component with a component type other than "module" when registering it, you need to specify it.<br>

- `stage`<br>
_Type_ : string<br>
You can name the stage (type) of the scan by:

```json
{
    "stage": "Testing",
    "chipType" : "RD53A",
    ...
}
```

!!! Note
    In case of the scan for QC, this "stage" corresponds to the testing stage.<br>
    When you run a scan in QC mode, the current stage of the component loaded from the Local DB is automatically assigned, so you no need to set it.


