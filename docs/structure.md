# Database name list
* **localdb** <br>
Main database for YARR DB

* **localdbtools** <br>
Database for using in localDB tools e.g.) _synchronization DB_ function

# Data Structure

## **localdb**

![localdb_structure](images/db_structure.png)

# Collections (= tables in SQL) name list
## in **localdb**
* [**chip**](db-chip.md) <br>
Tested chip information

* [**component**](db-component.md) <br>
Registered component (chips/modules) information

* [**childParentRelation**](db-childParentRelation.md) <br>
Relationship between chips and modules 

* [**testRun**](db-testRun.md) <br>
Test information

* [**componentTestRun**](db-componentTestRun.md) <br>
Relationship between chip/component and testRun

* [**config**](db-config.md) <br>
Config information

* [**user**](db-user.md) <br>
User information

* [**institution**](db-institution.md) <br>
Site information

* [**environment**](db-environment.md) <br>
DCS information

* [**fs.files**](db-GridFS.md) (GridFS) <br>
Binary (text) File information

* [**fs.chunks**](db-GridFS.md) (GridFS) <br>
Binary (text) File chunks
