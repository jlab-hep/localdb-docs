# DCS Config

You can specify the configuration of the DCS data when uploading data into Local DB.<br>

### DCS Config File

#### File Format

The DCS configuration file uses the JSON format:

```json
{
    "environments": [{
        "description": "VDDD Voltage [V]",
        "key": "vddd_voltage",
        "num": 0,
        "path": "dcs.dat",
        "status": "enabled"
    },{
        "description": "VDDD Current [A]",
        "key": "vddd_current",
        "num": 0,
        "path": "dcs.dat",
        "status": "disabled"
    }]
}
```

#### Options

##### Core Options

- `status`<br>
_Type_ : string<br>
Set enabled/disabled to upload the DCS data.

- `key`<br>
_Type_ : string<br>
Specifies a DCS keyword to upload.<br>
The keyword must be written in the ["environment" list in database config file](database.md), and the list can be changed under the responsibility of the user.

- `num`<br>
_Type_ : int<br>
Specifies a DCS data number.<br>
This number must be unique among data with the same DCS keyword.<br>
The combination of the DCS keyword and this number are used to specify the DCS data in the provided [DCS data file](#dcs-data-file).

- `description`<br>
_Type_ : string<br>
Adds a description of the DCS data.<br>
This description will be displayed on the viewer application and help us undeerstand what this data is.

- `path`<br>
_Type_ : string<br>
Specifies a path to [DCS data file](#dcs-data-file).

##### Aditional Options

- `value`<br>
_Type_ : float<br>
Specifies a single DCS value instead of providing the DCS data file.

- `mode`<br>
_Type_ : string<br>
Adds a description about a mode of DCS setting. (e.g. CV)

- `setting`<br>
_Type_ : float, string<br>
Adds a DCS setting parameter.

- `chip`<br>
_Type_ : string<br>
Specifies the chip name related with DCS data to link the data to the chip itself and upload it.<br>
If not specified, DCS data is uploaded associated with all chips tested in the scan.

### influxDB Config File

#### File Format

The DCS configuration file for influxDB uses the JSON format:

```json
{
    "environments" : [{
        "measurement" : "qaqcTest",
        "dcsList" : [{
            "key"        : "vddd_voltage",
            "data_name"  : "vdddVoltage",
            "description": "the voltage"
        },{
            "key"        : "vddd_current",
            "data_name"  : "vdddCurrent",
            "description": "the current"
        }]
    }]
}
```

#### Options

##### Core Options

- `measurement`<br>
_Type_ : string<br>
Set the measurement where the data is stored in InfluxDB.

- `key`<br>
_Type_ : string<br>
Specifies a DCS keyword to upload.<br>
The keyword must be written in the ["environment" list in database config file](database.md), and the list can be changed under the responsibility of the user.

- `data_name`<br>
_Type_ : string<br>
Specifies the title of the influxDB column where to take the data from.

- `description`<br>
_Type_ : string<br>
Adds a description of the DCS data.<br>
This description will be displayed on the viewer application and help us undeerstand what this data is.

### DCS Data File

#### File Format

The DCS data file uses DAT format:

```dat
key unixtime vddd_voltage vddd_current vdda_voltage vdda_current
num null 0 0 0 0
2019-06-24_20:49:13 1561376953 10 20 0 0
2019-06-24_20:49:23 1561376963 11 21 0 0
2019-06-24_20:49:33 1561376973 12 22 0 0
2019-06-24_20:49:43 1561376983 13 23 0 0
2019-06-24_20:49:53 1561376993 14 24 0 0
2019-06-24_20:50:03 1561377003 15 25 0 0
```

or CSV format:

```csv
key,unixtime,vddd_voltage,vddd_current,vdda_voltage,vdda_current,
num,null,0,0,0,0,
2019-06-24_20:49:13,1561376953,10,20,0,0,
2019-06-24_20:49:23,1561376963,11,21,0,0,
2019-06-24_20:49:33,1561376973,12,22,0,0,
2019-06-24_20:49:43,1561376983,13,23,0,0,
2019-06-24_20:49:53,1561376993,14,24,0,0,
2019-06-24_20:50:03,1561377003,15,25,0,0,
```

#### Syntax Rules

Separate each word with a space for DAT files and a comma for CSV files.

- the 1st line<br>
_Value_ : DCS keyword<br>
_DAT_ : `key unixtime <key1> <key2> <key3> ...`<br>
_CSV_ : `key,unixtime,<key1>,<key2>,<key3>,...`

- the 2nd line<br>
_Value_ : DCS number<br>
_DAT_ : `num null <num1> <num2> <num3> ...`
_CSV_ : `num,null,<num1>,<num2>,<num3>,...`

- After the 3rd line<br>
_Value_ :  datetime and DCS data (data value must be the number of the value or "null" if no data)<br>
_DAT_ : `datetime unixtime <data1> <data2> <data3> ...`<br>
_CSV_ : `datetime,unixtime,<data1>,<data2>,<data3>,...`
