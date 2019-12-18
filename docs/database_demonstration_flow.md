# Database Demonstration

## memo

- ITkPD URL

[https://itkpd-test.unicorncollege.cz](https://itkpd-test.unicorncollege.cz)

- YARR Docs

[https://yarr.readthedocs.io/en/latest/](https://yarr.readthedocs.io/en/latest/)

- YARR Repository

[https://gitlab.cern.ch/YARR/YARR/](https://gitlab.cern.ch/YARR/YARR/)

- Local DB Tools Repository

[https://gitlab.cern.ch/YARR/localdb-tools](https://gitlab.cern.ch/YARR/localdb-tools)

## Flow

In DB demonstration, we can do as follow things:

1. [pre requirements](database_demonstration_requirements.md)
    - Install the requirements for DB demonstration <br>( _We support CentOS, MacOS, Ubuntu, Windows_ )
2. [Set-up](database_demonstration_setup.md)
    - MongoDB
    - influxDB
    - Grafana
    - Viewer Application
    - YARR SW for Local DB
3. [Module Registration](database_demonstration_register_itkpd.md)
    - Register the module data into ITkPD (as test)
4. [Module Download](database_demonstration_download_itkpd.md)
    - Download the module data into Local DB from ITkPD (as test)
5. [scanConsole & Upload](database_demonstration_scanconsole.md)
    - Run scanConsole with uploading the test data into Local DB
6. [Viewer Application](database_demonstration_viewer.md)
    - Check the uploaded data in the Viewer Application
7. [Test Upload into ITkPD](database_demonstration_upload_itkpd.md)
    - Upload the test data into ITkPD (if possible)

![demo flow](images/demo_flow.png)
