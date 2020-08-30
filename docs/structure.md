## Database name list
* **localdb** <br>
Main database for YARR DB

* **localdbtools** <br>
Database for using in localDB tools e.g.) _synchronization DB_ function

## Data Structure

![localdb_structure](images/localdb/structure.png)

## Collections (= tables in SQL) name list

### **localdb**

* [**chip**](structure/chip.md) <br>
Tested chip information

* [**component**](structure/component.md) <br>
Registered component (chips/modules) information

* [**childParentRelation**](structure/childParentRelation.md) <br>
Relationship between chips and modules

* [**testRun**](structure/testRun.md) <br>
Test information

* [**componentTestRun**](structure/componentTestRun.md) <br>
Relationship between chip/component and testRun

* [**config**](structure/config.md) <br>
Config information

* [**user**](structure/user.md) <br>
User information

* [**institution**](structure/institution.md) <br>
Site information

* [**environment**](structure/environment.md) <br>
DCS information

* [**fs.files**](structure/GridFS.md) (GridFS) <br>
Binary (text) File information

* [**fs.chunks**](structure/GridFS.md) (GridFS) <br>
Binary (text) File chunks
