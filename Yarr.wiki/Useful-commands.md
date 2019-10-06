### Usefule commands for mongo DB client

First connect to mongo DB server,for example type `mongo`

* **show dbs**: <br>
List all database name

* **use \<database name\>**: <br>
switch to specific database. e.g.) `use yarrdb`

* **db.getCollectionNames()**: <br>
List all collection name in the specific database.

* **db.\<collection name\>.find()**: <br>
Output all data in the specific collection. e.g.)`db.component.find()`. If you want to more pretty output, add 'pretty()' from behind. e.g.)`db.component.find().pretty()`
