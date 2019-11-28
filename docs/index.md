![Local DB](images/logo.png)

## What is Local DB?
Local DB (Local Database) is the data management/storage system based on [MongoDB](https://docs.mongodb.com/) for [YARR](https://gitlab.cern.ch/YARR).<br>
Using the tools for Local DB, you can:

- **Store** the test data associated with some information; chip, user, site ...
- **Retrieve** the config or result data into local directory
- **Check** the data on browser via web interface
- **Share/Centralize** the data with other Local DB
- **Upload/Download** the data to/from Production Database

![Local DB System Overview](images/overview.png)

## Local DB System

|Function              |Tool Name           |System        |How to use                                |
|:--------------------:|:------------------:|:------------:|:----------------------------------------:|
|Storage System        |Local DB            |MongoDB       |[MongoDB Docs](https://docs.mongodb.com/) |
|Scan                  |scanConsole         |YARR          |[scanConsole Page](scanconsole.md)        |
|Store Data            |Upload Tool         |YARR          |[Upload Tool Page](upload.md)             |
|Restore Data          |Retrieve Tool       |YARR          |[Retrieve Tool Page](retrieve.md)         |
|Handle DB             |DB Accessor         |YARR          |[DB Accessor Page](accessor.md)           |
|Share Data            |Synchronization Tool|Local DB Tools|[Synchronization Tool Page](sync.md)      |
|Check Data            |Viewer Application  |Local DB Tools|[Viewer Application Page](viewer.md)      |
|Archive DB            |Archive Tool        |Local DB Tools|[Archive Tool Page](archive.md)           |
|Communicate with ITkPD|ITkPD Interface     |Local DB Tools|[ITkPD Interface Page](itkpd-interface.md)|

## Supported OS

* centOS7

## Folder Structure
```bash
YARR : Cloned from https://gitlab.cern.ch/YARR/YARR.git
|-- localdb
|   |-- setting                  : setup scripts and default config files dir
|   |-- bin                      : binary commands dir
|   |   |-- localdbtool-upload   : uploader
|   |   `-- localdbtool-retrieve : retriever
|   `-- lib                      : libaries dir
`-- bin                          : YARR read-out commands dir

localdb-tools : Cloned from https://gitlab.cern.ch/YARR/localdb-tools.git
|-- setting         : setup scripts dir
|-- viewer          : Viewer Application command & libraries
|-- sync-tool       : Synchronization Tool command & libraries
|-- archive-tool    : Archive Tool command & libraries
|-- itkpd-interface : ITkPD Interface command & libraries
|-- scripts         : Some scripts and default config files dir
`-- dev             : development dir
```

## Contact
|Role     |Name           |Institution                                                                        |E-mail                                 |
|:-------:|:-------------:|:---------------------------------------------------------------------------------:|:-------------------------------------:|
|Developer|Hiroki Okuyama |[Tokyo Institute of Technology](http://www-hep.phys.titech.ac.jp/jlab/index_e.html)|hiroki.okuyama(at)cern.ch              |
|Developer|Alisa Kubota   |[Tokyo Institute of Technology](http://www-hep.phys.titech.ac.jp/jlab/index_e.html)|arisa.kubota(at)cern.ch                |
|Developer|Eunchong Kim   |[Tokyo Institute of Technology](http://www-hep.phys.titech.ac.jp/jlab/index_e.html)|eunchong.kim(at)cern.ch                |
|Developer|Shohei Yamagaya|[Osaka University](http://osksn2.hep.sci.osaka-u.ac.jp/member.html)                |yamagaya(at)champ.hep.sci.osaka-u.ac.jp|
|Developer|Hideyuki Oide  |[Tokyo Institute of Technology](http://www-hep.phys.titech.ac.jp/jlab/index_e.html)|hideyuki.oide(at)cern.ch               |

## Production Tags

|Tag            |Version|Date             |Describe                                                                 |
|:-------------:|:-----:|:---------------:|:-----------------------------------------------------------------------:|
|-              |-      |-                |=                                                                        |
|ldbtoolv1.1    |1.1    |2018-10---       |First relase (Latest stable version)                                     |
|ldbtoolv1.0    |1.01   |2018-08---2018-10|Merged into YARR/devel                                                   |
|-              |1.00   |2018-06---2018-08|Updating version (Very Unstable)                                         |
|db-v0.8        |0.80   |2018-03---2018-06|Unstable database version                                                |
|old-db-v       |0.15   |-                |Old database version based on latest YARR software                       |
|old-sw-old-db-v|0.10   |-                |Old database version based on old software version (YARR/master 7c4a0727)|

## Working Branch
|Project       |Branch       |Describe                          |Link                                                        |
|:------------:|:-----------:|:--------------------------------:|:----------------------------------------------------------:|
|YARR          |master       |Stable DAQ SW                     |[Git](https://gitlab.cern.ch/YARR/YARR/tree/master)         |
|YARR          |devel        |Latest DAQ SW                     |[Git](https://gitlab.cern.ch/YARR/YARR/tree/devel)          |
|YARR          |devel-localdb|Latest DB SW based on devel branch|[Git](https://gitlab.cern.ch/YARR/YARR/tree/devel-localdb)  |
|Local DB Tools|master       |Stable Local DB Tools SW          |[Git](https://gitlab.cern.ch/YARR/localdb-tools/tree/master)|
|Local DB Tools|devel        |Latest Local DB Tools SW          |[Git](https://gitlab.cern.ch/YARR/localdb-tools/tree/devel) |
