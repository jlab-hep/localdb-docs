You can check data in database via web interface with [viewer application](https://gitlab.cern.ch/akubota/web-app-db-yarr/blob/master/README.md
) powered by Python and Flask with PyMongo python module.
> requirements
>* centOS7
>* local database is running
>* ROOT software
>* python 2.X or 3.X which can use PyROOT

# Ready
## 0) environmental setting
   ```
   $ source path/to/devtoolset-2/enable
   $ source path/to/bin/thispython.sh
   $ source path/to/bin/thisroot.sh
   ```

## 1) Install pip and modules

1) Download web-app-db-yarr
   ```
   $ cd /var/www
   $ git clone https://gitlab.cern.ch/akubota/web-app-db-yarr.git
   $ cd web-app-db-yarr
   $ git checkout devel-latest
   $ cd ../
   $ chown -R $USER web-app-db-yarr
   $ chgrp -R $USER web-app-db-yarr
   ```

2) Install pip
   * python2
     ```
     $ sudo yum install epel-release
     $ sudo yum install python python-pip poppler-utils
     ```

   * python3
     ```
     sudo yum install epel-release
     sudo yum install python36 python36-devel python36-setuptools
     sudo easy_install-3.6 pip
     ```

   * In case of none-sudo user, do below to install on local.
     ```
     $ curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
     $ python get-pip.py --user
     ```

3) Install python modules
   ```
   $ cd web-app-db-yarr/scripts/install
   $ ./make_pipinstall.sh    # change PIPPATH in this script if you use python3
   $ sudo python pipinstall.py
   ```

## 2) Create configuration file
   ```
   $ cd web-app-db-yarr
   $ cp scripts/yaml/web-conf.yml conf.yml
   ```

# Usage
   Check [Quick tutorial for Viewer](https://github.com/jlab-hep/Yarr/wiki/Quick-tutorial-for-Viewer)

---

# Advance : apache

The viewer can be accessed via apache. 

## 1) Configure apache2

   ```
   $ cd /var/www/web-app-db-yarr
   $ sudo cp scripts/apache/config.conf /etc/httpd/conf.d/web-app-db-yarr.conf
   ```

   If you want to limit where to access the viewer, remove comment out and add `Allow from XXX`.

   For example, in case you allow access from `ac.jp`, you change the config file as below:
   ```
   <Proxy *>
       Order deny,allow
       Deny from all
       Allow from ac.jp
   #    Allow from all
   </Proxy>
   <Location /yarrdb/>
       Order deny,allow
       Deny from all
       Allow from ac.jp
   #    Allow from all
   </Location>
   <VirtualHost *:80>
     ProxyPreserveHost On
     ProxyRequests Off
     ProxyPass /yarrdb/ http://localhost:5000/yarrdb/
     ProxyPassReverse /yarrdb/ http://localhost:5000/yarrdb/
   </VirtualHost>
   ```

## 2) Allow httpd make network request
   This allows apache connect to mongo server
   ```
   $ sudo /usr/sbin/setsebool -P httpd_can_network_connect 1
   ```

## 3) Restart apache service
   ```
   $ sudo systemctl start httpd
   $ sudo systemctl enable httpd
   ```

## 4) Open 80 port if need
   ```
   sudo firewall-cmd --add-service=http --permanent
   sudo firewall-cmd --reload
   ```