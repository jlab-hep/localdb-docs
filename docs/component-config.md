# Component Config

You can specify the configuration of the component data when registering the component data into Local DB.

#### File Format

The component configuration file uses the JSON format.

##### SCC

```json
{
    "chipType" : "RD53A",
    "chips" : [
        {
            "serialNumber": "RD53A-001",
            "componentType": "Front-end Chip",
            "chipId": 0
        }
    ]
}
```

##### Quad

```json
{
    "module": {
        "serialNumber": "RD53A-001",
        "componentType": "Module"
    },
    "chipType" : "RD53A",
    "chips" : [
        {
            "serialNumber": "RD53A-001-001",
            "componentType": "Front-end Chip",
            "chipId": 1
        },
        {
            "serialNumber": "RD53A-001-002",
            "componentType": "Front-end Chip",
            "chipId": 2
        },
        {
            "serialNumber": "RD53A-001-003",
            "componentType": "Front-end Chip",
            "chipId": 3
        },
        {
            "serialNumber": "RD53A-001-004",
            "componentType": "Front-end Chip",
            "chipId": 4
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
Specifies the chips to register.
    - `serialNumber`<br>
      _Type_ : string<br>
      Specifies the serial number of the chip component.
    - `chipId`/`ChipId`<br>
      _Type_ : int<br>
      Specifies the geometrical ID determined by wirebonding.
    - `componentType`<br>
      _Type_ : string<br>
      If you want to register the component with a component type other than "Front-end Chip", you can specify it.

##### Addtional Options

- `module`<br>
_Type_ : dictionary<br>
Specifies the module to register.
    - `serialNumber`<br>
      _Type_ : string<br>
      Specifies the serial number of the module component.
    - `componentType`<br>
      _Type_ : string<br>
      If you want to register the component with a component type other than "module", you can specify it.<br>
