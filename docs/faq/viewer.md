# Viewer

### Table of Contents

- [How to Set Apache](#how-to-set-apache)

---

## How to Set Apache

You can run the [viewer application](tool/viewer.md) using apache service.

###### 1. Install Apache2 and WSGI

```bash
$ sudo yum install httpd
$ sudo yum install centos-release-scl
$ sudo yum install rh-python36-mod_wsgi
$ sudo yum remove mod_wsgi.x86_64
```

!!! Warning
    Do not install `sudo yum install mod_wsgi` because it will install for python2, not for python3.

###### 2. Set security

Open port 80 and 443:

```bash
$ sudo firewall-cmd --add-service=http --permanent
$ sudo firewall-cmd --add-service=https --permanent
$ sudo firewall-cmd --reload
```

Set SELinux boolean **httpd_can_network_connect**:

```bash
$ sudo /usr/sbin/setsebool -P httpd_can_network_connect 1
```

!!! Note
    See the [description about SELinx](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/security-enhanced_linux/sect-security-enhanced_linux-working_with_selinux-selinux_contexts_labeling_files).

###### 3. Set Local DB Viewer

Clone Local DB Tools:

```bash
$ cd /var/www
$ sudo git clone https://gitlab.cern.ch/yarr/localdb-tools.git
$ sudo chown -R ${USER} localdb-tools
```

Setup the [viewer application](tool/viewer.md):

```bash
$ cd /var/www/localdb-tools/setting
$ ./create_admin.sh
$ cd /var/www/localdb-tools/viewer
$ ./setup_viewer.sh
$ sudo chmod +x admin_conf.yml .KeyFile
```

Set SELinux boolean **httpd_sys_content_t**, **httpd_sys_script_exec_t**, and **ihttpd_execmem**:

```bash
$ sudo semanage fcontext -a -t httpd_sys_content_t '/var/www/localdb-tools/viewer(/.*)?'
$ sudo semanage fcontext -a -t httpd_sys_script_exec_t '/var/www/localdb-tools/viewer/plotting-tool/bin(/.*)?'
sudo semanage fcontext -a -t httpd_sys_script_exec_t '/var/www/localdb-tools/viewer/analysis-tool/bin(/.*)?'
$ sudo restorecon -R /var/www/localdb-tools/
$ sudo setsebool -P httpd_execmem on
```

###### 4. Setup apache2

There are three types of apache configurations supported by the Local DB system:

- apache w/o SSL authentication certificate
- apache w/ SSL authentication certificate
- proxy server (w/o WSGI)

###### 4-a. w/o SSL authentication certificate

Setup apache2 config:

```bash
$ sudo cp /var/www/localdb-tools/setting/apache2/viewer_http.conf /etc/httpd/conf.d/.
$ sudo sed -i -e "s/HOSTNAME/${HOSTNAME}/g" /etc/httpd/conf.d/viewer_http.conf
```

###### 4-b. w/ SSL authentication certificate

Create SSL authentication certificate file:

```bash
$ sudo yum install mod_ssl
$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/pki/tls/private/localdb-viewer.key -out /etc/pki/tls/certs/localdb-viewer.crt

#   Country Name (2 letter code) [XX]:US
#   State or Province Name (full name) []:Example
#   Locality Name (eg, city) [Default City]:Example
#   Organization Name (eg, company) [Default Company Ltd]:Example Inc
#   Organizational Unit Name (eg, section) []:Example Dept
#   Common Name (eg, your name or your server's hostname) []:example.com
#   Email Address []:webmaster@example.com

$ sudo openssl dhparam -out /etc/pki/tls/certs/dhparam.pem 2048
$ cat /etc/pki/tls/certs/dhparam.pem | sudo tee -a /etc/pki/tls/certs/localdb-viewer.crt
```

Setup apache2 config:

```bash
$ sudo cp /var/www/localdb-tools/setting/apache2/viewer_https.conf /etc/httpd/conf.d/.
$ sudo sed -i -e "s/HOSTNAME/${HOSTNAME}/" /etc/httpd/conf.d/viewer_https.conf
$ sudo cp /var/www/localdb-tools/setting/apache2/viewer_http_https.conf /etc/httpd/conf.d/viewer_http.conf
$ sudo sed -i -e "s/HOSTNAME/${HOSTNAME}/g" /etc/httpd/conf.d/viewer_http.conf
```

###### 4-c. proxy server

Setup apache2 config:

```bash
$ sudo cp /var/www/localdb-tools/setting/apache2/viewer_http_proxy.conf /etc/httpd/conf.d/viewer_http.conf
```

Run the viewer application locally:

```bash
$ cd /var/www/localdb-tools/viewer
$ ./app.py --config admin_conf.yml 1>viewer.log 2>&1 &
```

###### 5. Run apache2

```bash
$ sudo chown -R apache:apache /var/www/localdb-tools
$ sudo systemctl restart httpd.service
```

###### 6. Open browser and check the viewer application (e.g. http://localhost/localdb)
