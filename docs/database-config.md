# Database Config

You can specify the configuration of Local DB when connecting using a configuration file.

#### File Format

Local DB configuration file uses the JSON format:

```json
{
    "hostIp": "127.0.0.1",
    "hostPort": "27017",
    "dbName": "localdb",
    "auth": "default",
    "KeyFile": "null",
    "QC": false,
    "environment": [
        "vddd_voltage",
        "vddd_current",
        "vdda_voltage",
        "vdda_current",
        "vddcom_voltage",
        "vddcom_current",
        "hv_voltage",
        "hv_current",
        "temperature"
    ]
}
```

#### Options

##### Core Options

- `hostIp`<br>
_Type_ : string<br>
_Default_ : "127.0.0.1"<br>
Specifies the name or IP addres of the host machine where the Local DB is running.

- `hostPort`<br>
_Type_ : string<br>
_Default_ : "27017"<br>
Specifies the port number where the Local DB is listening.

- `dbName`<br>
_Type_ : string<br>
_Default_ : "localdb"<br>
Specified the name of the database registered as Local DB in MongoDB to connect to.

- `auth`<br>
_Type_ : string<br>
_Default_ : "default"<br>
Specifies the authentication mode used in MongoDB.<br>
If this is not specified, specifies ["default" (SCRAM)](https://docs.mongodb.com/manual/core/security-scram/#authentication-scram), the default authenrication mechanism for MongoDB.<br>
If you use [x.509 certificate authentication](https://docs.mongodb.com/manual/core/security-x.509/#security-auth-x509) you need to specify "x509" here.

- `QC`<br>
_Type_ : boolean<br>
_Default_ : False<br>
If you want to upload data for QC, you need to set **true** here.<br>

- `Environment`<br>
_Type_ : list<br>
The DCS data with a key listed here can be registered in Local DB.<br>
If you want to register other DCS data, you need to add key here.

##### SSL/TLS Options

```json
{
    "ssl": {
        "enabled": false,
        "PEMKeyFile": "path/to/mongodb.pem",
        "CAFile": "path/to/ca.pem"
    }
}
```

- `ssl.enabled`<br>
If Local DB server uses SSL connection, set **true** here.

- `ssl.PEMKeyFile`<br>
Specifies the .pem file that contains both the SSL certificate and key to present to the Local DB server.

- `ssl.CAFile`<br>
Specifies the .pem file that contaibns the root certificate chain from the Certificate Authority to validate the server certificate.

##### TLS Options

```json
{
    "tls": {
        "enabled": false,
        "CertificateKeyFile": "path/to/mongodb.pem",
        "CAFile": "path/to/ca.pem"
    }
}
```

- `tls.enabled`<br>
If Local DB server uses TLS connection, set **true** here.

- `tls.CertificateKeyFile`<br>
Specifies the .pem file that contains both the TLS certificate and key to present to the Local DB server.

- `tls.CAFile`<br>
Specifies the .pem file that contaibns the root certificate chain from the Certificate Authority to validate the server certificate.
