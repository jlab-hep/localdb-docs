# Archive Tool Config

You can specify the configuration of Local DB server to archive it.

#### File Format

Archive Tool configuration file uses the YAML format:

```yml
data_path: /var/lib/mongo
archive_path: /root/archive-mongo-data
n_archives: 2
```

#### Options

- `data_path`<br>
_Default_ : /var/lib/mongo<br>
Specifies path to MongoDB database.

- `archive_path`<br>
_Default_ : ./archive-mongo-data<br>
Specifies path to put archives (Recommendation: use external HDD/SSD)

- `n_archive`<br>
_Default_ : 2<br>
Specifies the number of archives want to keep (It depends on size of your disk storage)
