# Database name list
* **localdb** <br>
Main database for YARR DB

* **localdbtools** <br>
Database for using in localDB tools e.g.) _synchronization DB_ function

# Data Structure

## **localdb**

![localdb_structure](images/localdb_structure.png)

# Collections (= tables in SQL) name list
## in **localdb**
* [**component**](https://github.com/jlabhep/Yarr/wiki/component) <br>
Component information of chips and modules 

* [**childParentRelation**](https://github.com/jlabhep/Yarr/wiki/childParentRelation) <br>
Relationship between chips and modules 

* [**testRun**](https://github.com/jlabhep/Yarr/wiki/testRun) <br>
Test (scan) information for each component with attachments information

* [**componentTestRun**](https://github.com/jlabhep/Yarr/wiki/componentTestRun) <br>
Relationship between component and testRun

* [**config**](https://github.com/jlabhep/Yarr/wiki/config) <br>
Config file information

* [**user**](https://github.com/jlabhep/Yarr/wiki/user) <br>
User information

* [**institution**](https://github.com/jlabhep/Yarr/wiki/institution) <br>
Site information

* [**environment**](https://github.com/jlabhep/Yarr/wiki/environment) <br>
DCS information

* [**fs.files**](https://github.com/jlabhep/Yarr/wiki/GridFS) (GridFS) <br>
Binary (text) File information

* [**fs.chunks**](https://github.com/jlabhep/Yarr/wiki/GridFS) (GridFS) <br>
Binary (text) File chunks
