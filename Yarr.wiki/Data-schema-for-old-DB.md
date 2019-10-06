# Database name list
* **yarrdb** <br>
Main database for YARR DB

* **yarrdbsync** <br>
Database for using _synchronization DB_ function

* **userdb** <br>
Database for web viewer to store user information


# Collections (= tables in SQL) name list
## in **yarrdb**
* **component** <br>
Component information of chips and modules 

* **childParentRelation** <br>
Relationship between chips and modules 

* **testRun** <br>
Test (scan) information for each component with attachments information

* **componentTestRun** <br>
Relationship between component and testRun

* **fs.files** (GridFS) <br>
Binary (text) File information

* **fs.chunks** (GridFS) <br>
Binary (text) File chunks
