### Connectivity cfg

- `stage` : The test stage, which should be selected from the stage list written in [database.json](#database-cfg)
- `module` : configures for module (option)<br>**Must be set when uploading the test data in association with the MODULE.**
- `chipType` : "FEI4B" or "RD53A"
- `chips.i` : configures for chip
    - `serialNumber` : The serial number of the module/chip.<br>**Ensure the same as 'Name' written in chip config file.**
    - `config` : The path to chip config file (only in `chip.i`)
    - `tx` : The TX channel, which must be "int" (only in `chip.i`)
    - `rx` : The RX channel, which must be "int" (only in `chip.i`)

#### For RD53A

```json
{
    "stage": "Testing",
    "chipType" : "RD53A",
    "chips" : [
        {
            "serialNumber": "RD53A-001",
            "config" : "configs/chip1.json",
            "tx" : 0,
            "rx" : 0
        }
    ]
}
```
#### For FEI4B

```json
{
    "stage": "Testing",
    "module": {
        "serialNumber": "FEI4B-001"
    },
    "chipType" : "FEI4B",
    "chips" : [
        {
            "serialNumber": "FEI4B-001-chip1",
            "config" : "configs/chip1.json",
            "tx" : 0,
            "rx" : 0
        },
        {
            "serialNumber": "FEI4B-001-chip2",
            "config" : "configs/chip2.json",
            "tx" : 0,
            "rx" : 1
        },
        {
            "serialNumber": "FEI4B-001-chip3",
            "config" : "configs/chip3.json",
            "tx" : 0,
            "rx" : 2
        },
        {
            "serialNumber": "FEI4B-001-chip4",
            "config" : "configs/chip4.json",
            "tx" : 0,
            "rx" : 3
        }
    ]
}
```


