## Requirements
  * centOS7
  * user account who is authorized for sudo in computer
  * git
    ```
    $ sudo yum install git
    ```

## Installer
   You can install and compile following software and start mongodb and httpd server by this installer : 
`db_install.sh`
   * libraries and server system (python27, mongodb36, apache ... ref: [Install libraries](https://github.com/jlab-hep/Yarr/wiki/Install-libraries))
   * Yarr software for database (ref: [Compile YARR SW](https://github.com/jlabhep/Yarr/wiki/Conmpile-YARR-SW))
   * Viewer application software (ref: [Web interface](https://github.com/jlabhep/Yarr/wiki/Web-interface))

   usage)
   ```
   $ git clone https://gitlab.cern.ch/hirose/mongodb_install.git
   $ cd mongodb_install
   $ ./db_install.sh <FEI4/RD53> [<dir_name>]        # e.g. for RD53) $ ./db_install.sh RD53 
   [2019-01-01 01:01:01]  Yarr-<FEI4/RD53> software will be installed in: ./Yarr_<FEI4/RD53>
   [2019-01-01 01:01:01]  Start installing necessary packages...
   [sudo] password for user: XXXXXXXX        # Enter password

   ---> Yarr SW for <asic_type> will be installed in ./<dir_name> with argument or ./Yarr_<FEI4/RD53> without argument
   ---> Viewer application SW will be installed in /var/www/web-app-db-yarr
   ```

  After installation, you can upload data into database with Yarr SW and check them with Viewer application following tutorials:
  * [usage for Yarr SW](https://github.com/jlab-hep/Yarr/wiki/Quick-tutorial-for-Yarr)
  * [usage for Viewer app](https://github.com/jlab-hep/Yarr/wiki/Quick-tutorial-for-Viewer)
## For Manual Installation
  * [Install libraries](https://github.com/jlab-hep/Yarr/wiki/Install-libraries)
  * [Compile YARR SW](https://github.com/jlabhep/Yarr/wiki/Conmpile-YARR-SW)
  * [Install and start server](https://github.com/jlab-hep/Yarr/wiki/Install-and-start-server)
  * [Web interface](https://github.com/jlabhep/Yarr/wiki/Web-interface)