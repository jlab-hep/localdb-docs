# Chip Config

You can specify the configuration of the chip when executing the scan and uploading data into Local DB.<br>
You can check the default format of the chip config file in `YARR/configs/defaults/<FE>.json`.

#### File Format

The chip configuration file uses the JSON format.

##### FEI4B

```json
{
    "FE-I4B": {
        ...
        "Parameter": {
            ...
            "chipId": 0
        },
        "name": "FEI4B-001"
    }
}
```

##### RD53A

```json
{
    "RD53A": {
        ...
        "Parameter": {
            ...
            "ChipId": 0,
            "Name": "RD53A-001"
        }
    }
}
```

#### Options

- `name`/`Name`<br>
_Type_ : string<br>
Specifies the name (serial number) of the chip component.

- `chipId`/`ChipId`<br>
_Type_ : int<br>
Specifies the geometrical ID determined by wirebonding.
