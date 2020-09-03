## SSL/TLS Connection

See the [MongoDB docs: TLS/SSL](https://docs.mongodb.com/manual/tutorial/configure-ssl/) to get more detail.

#### a) Requirements for DB Server

###### 1. Open the TCP port (e.g. 27017) used by mongod service

```bash
$ sudo firewall-cmd --zone=public --add-port=27017/tcp --permanent
$ sudo firewall-cmd --reload
```

###### 2. Create x.509 certificate for server

See
[MongoDB docs: Create CA PEM file](https://docs.mongodb.com/manual/appendix/security/appendixA-openssl-ca/)
and
[MongoDB docs: Create Server Certificates](https://docs.mongodb.com/manual/appendix/security/appendixB-openssl-server/#appendix-server-certificate).

```bash
$ sudo cp path/to/CA/file /etc/ssl/localdb_ca.pem
$ sudo cp path/to/certificate/file /etc/ssl/localdb_cert.pem
```

###### 3. Stop MongoDB

```bash
$ sudo systemctl stop mongod
$ sudo vim /etc/mongod.conf
```

###### 4. Set SSL/TLS mode

###### 4.1 Set SSL mode(For MongoDB version 4.0 and earlier)

```yaml
# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1,"DB SERVER HOSTNAME"
  ssl:
    mode: requireSSL
    PEMKeyFile: /etc/ssl/localdb_cert.pem ### Server Certificate
    CAFile: /etc/ssl/localdb_ca.pem ### CA PEM File
```

###### 4.2 Set TLS mode (For MongoDB version 4.2 and greater)

```yaml
# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1, "DB SERVER HOSTNAME"
  tls:
    mode: requireTLS
    certificateKeyFile: /etc/ssl/localdb_cert.pem ### Server Certificate
    CAFile: /etc/ssl/localdb_ca.pem ### CA PEM File
```

###### 5. Start MongoDB

```bash
$ sudo systemctl restart mongod.service
```

###### 6. Confirmation

```bash
# For MongoDB version 4.0 and earlier
$ mongo --ssl --sslPEMKeyFile /etc/ssl/localdb_cert.pem --sslCAFile /etc/ssl/localdb_ca.pem --sslAllowInvalidHostnames --port 27017
# For MongoDB version 4.2 and greater
$ mongo --tls --tlsCertificateKeyFile /etc/ssl/localdb_cert.pem --tlsCAFile /etc/ssl/localdb_ca.pem --tlsAllowInvalidHostnames --port 27017
```

###### 7. Create x.509 certificate for client

See [MongoDB docs: Create Client Certificates](https://docs.mongodb.com/manual/appendix/security/appendixC-openssl-client/#appendix-client-certificate).<br>
Send the client certificate and CA file to the client machine.

#### b) Remote Connection from the client machine

###### 1. Receive x.509 certificate for client

###### 2. Confirmation

```bash
# For MongoDB version 4.0 and earlier
$ mongo --ssl --sslPEMKeyFile /etc/ssl/localdb_cert.pem --sslCAFile /etc/ssl/localdb_ca.pem --sslAllowInvalidHostnames --port 27017 --host "DB SERVER HOSTNAME"
# For MongoDB version 4.2 and greater
$ mongo --tls --tlsCertificateKeyFile /etc/ssl/localdb_cert.pem --tlsCAFile /etc/ssl/localdb_ca.pem --tlsAllowInvalidHostnames --port 27017 --host "DB SERVER HOSTNAME"
```


