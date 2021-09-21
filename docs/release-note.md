# Relase Note

##### Local DB Tools : [1.6.0](https://gitlab.cern.ch/YARR/localdb-tools/-/tree/ldbtoolv1.6.0)

##### YARR : [5ca0199d](https://gitlab.cern.ch/YARR/YARR/-/commit/5ca0199de9799695c7d5046a2bdcdff18d8e6847)


### New features
- Push QC test result to ITkPD
- Pull QC test result from ITkPD
- Show all types of scan result(e.g. source scan, tuning)
- Rename component's serial numbers with re-downloading the list of them

### What you can do with this version
- Provide an admin page
- Manage the information of users and QC testers
- Some user functions (comments, tags)
- Register/download module to/from ITkPD
- Supporting a part of the QC stages in the ProdDB (Module to PCB, Wirebonding)
- Show the results of QC test
  - non-electrical test
    - Bare to PCB Assembly (Optical Inspection, Metrology, Mass)
    - Wire-bonding (Optical Inspection, Sensor IV, SLDO VI, Wirebonding Information, Wirebond Pull Test IrefTrim, Pullup register, Orientation)
  - electrical test
    - YARR rerated scan
    - Pixel failure test
- Sign off QC test
- Upload/download QC test results to/from ITkPD
