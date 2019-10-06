# Local DB: Local Database

## What is Local DB?
Local DB is the local data management/storage system based on [MongoDB](https://docs.mongodb.com/) for [YARR](https://gitlab.cern.ch/YARR).<br>
Using the tools for Local DB, you can:

- Store the test data taken by YARR associated with some information; chip data, user data, site data ...
- Retrieve the config or result data into local directory
- Check the data on browser via web interface
- Share/Centralize the data with other Local DB
- Analysis the data and output the result data/plot
- Upload/Download the data to/from Production Database

## Base System
* [MongoDB](https://docs.mongodb.com/v4.0/) v4.X
* [YARR SW](https://gitlab.cern.ch/YARR/YARR)
* [Local DB Tools](https://gitlab.cern.ch/YARR/localdb-tools)

## Local DB Tools
|Function      |Tool Name           |Command             |
|:------------:|:------------------:|:------------------:|
|Storage System|Local DB            |mongo               |
|Store Data    |Upload Tool         |localdbtool-upload  |
|Restore Data  |Retrieve Tool       |localdbtool-retrieve|
|Share Data    |Synchronization Tool|localdbtool-sync    |
|Check Data    |Viewer Application  |python app.py       |

## Content
* [Software Installation](install.md)

## Contact

|Role|Name|Institution|E-mail|
|:--|:--|:--|:--|
|Developer|[Alisa Kubota](https://github.com/arisakubota)|[Tokyo Institute of Technology](http://www-hep.phys.titech.ac.jp/jlab/index_e.html)|arisa.kubota(a)cern.ch|
|Developer|[Hiroki Okuyama](https://github.com/hokuyama0106)|[Tokyo Institute of Technology](http://www-hep.phys.titech.ac.jp/jlab/index_e.html)|hiroki.okuyama(a)cern.ch|
|Developer|[Hideyuki Oide]()|[Tokyo Institute of Technology](http://www-hep.phys.titech.ac.jp/jlab/index_e.html)|hideyuki.oide(a)cern.ch|
|Developer|[Eunchong Kim](https://github.com/newini)|[Tokyo Institute of Technology](http://www-hep.phys.titech.ac.jp/jlab/index_e.html)|eunchong.kim(a)cern.ch|
