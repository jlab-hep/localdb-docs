This page describes how to register the module data into Local DB.
(<span style="color:red">PLAN: to be deleted and will prepare the script to download the component data from ITk PD.</span>) <br>

### Requirements

- DAQ Server with [required libraries installed](https://github.com/jlab-hep/Yarr/wiki/Installation)
- DB Server with [required libraries installed](https://github.com/jlab-hep/Yarr/wiki/Installation)
- Setup DAQ system: [setup_db.sh](https://github.com/jlab-hep/Yarr/wiki/Setup-DAQ-Server)
- Compile scanConsole 

```bash
$ cd YARR
$ git checkout devel
$ mkdir build-localdb
$ cd build-localdb
$ cmake3 ../
$ make -j4
$ make install
```

### Config files

Prepare the component information file and user information file.<br>

- user config file (json)

   **Required information**
   - userName: your name (e.g. "John Doe")
   - institution: institution you belong (e.g. "ABC Laboratory")
   - description: description for user account (e.g. "account for testbeam")
 
   <details><summary>user.json</summary><div>
 
   ```json
   {
     "userName": "FIRSTNAME LASTNAME",
     "institution": "INSTITUTION",
     "description": "default"
   } 
   ```
 
   </div></details>

- component config file (json)

   <span style="color:red">One file for one module!</span> 
 
   **Required information**
   - module.serialNumber: serial number of the module
   - module.componentType: "Module"
   - chipType: "FEI4B" or "RD53A"
   - chips: chips on the module
     - chips.i.serialNumber: serial number of the chip
     - chips.i.componentType: "Front-end Chip"
     - chips.i.chipId: chipID must be "int"
 
   <details><summary>component.json for RD53A</summary><div>
 
     ```json
     {
         "module": {
             "serialNumber": "RD53A-001",
             "componentType": "Module"
         },
         "chipType" : "RD53A",
         "chips" : [
             {
                 "serialNumber": "RD53A-001_chip1",
                 "componentType": "Front-end Chip",
                 "chipId": 0
             }
         ]
     }
     ```
 
   </div></details>
 
   <details><summary>component.json for FEI4B</summary><div>
 
     ```json
     {
         "module": {
             "serialNumber": "FEI4B-001",
             "componentType": "Module"
         },
         "chipType" : "FEI4B",
         "chips" : [
             {
                 "serialNumber": "FEI4B-001-chip1",
                 "componentType": "Front-end Chip",
                 "chipId": 1
             },
             {
                 "serialNumber": "FEI4B-001-chip2",
                 "componentType": "Front-end Chip",
                 "chipId": 2
             },
             {
                 "serialNumber": "FEI4B-001-chip3",
                 "componentType": "Front-end Chip",
                 "chipId": 3
             },
             {
                 "serialNumber": "FEI4B-001-chip4",
                 "componentType": "Front-end Chip",
                 "chipId": 4
             }
         ]
     }
     ```
 
   </div></details>

### Registration

Run the `dbAccessor -C` to register the components data written in component.json:

```bash
$ ./bin/dbAccessor -C component.json -u user.json
<some texts>
Do you continue to upload data into Local DB? [y/n]
y
#DB INFO# Completed the registration successfuly.
```

### Confirmation

```bash
$ localdbtool-upload check
#DB INFO# Local DB Server: mongodb://127.0.0.1:27017
#DB INFO# ---> connection is good.
#DB INFO# Download Component Data of Local DB locally...
#DB INFO# --------------------------------------
#DB INFO# Component (1)
#DB INFO#     Chip Type: FE-I4B
#DB INFO#     Module:
#DB INFO#         serial number: FEI4B-002
#DB INFO#         component type: Module
#DB INFO#         chips: 4
#DB INFO#     Chip (1):
#DB INFO#         serial number: FEI4B-002_chip1
#DB INFO#         component type: Front-end Chip
#DB INFO#         chip ID: 1
#DB INFO#     Chip (2):
#DB INFO#         serial number: FEI4B-002_chip2
#DB INFO#         component type: Front-end Chip
#DB INFO#         chip ID: 2
#DB INFO#     Chip (3):
#DB INFO#         serial number: FEI4B-002_chip3
#DB INFO#         component type: Front-end Chip
#DB INFO#         chip ID: 3
#DB INFO#     Chip (4):
#DB INFO#         serial number: FEI4B-002_chip4
#DB INFO#         component type: Front-end Chip
#DB INFO#         chip ID: 4
#DB INFO# --------------------------------------
#DB INFO# Done.
```

