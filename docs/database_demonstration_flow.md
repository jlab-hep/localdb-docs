# Database Demonstration

## memo

- [ITkPD URL](https://itkpd-test.unicorncollege.cz)
- [YARR Docs](https://yarr.readthedocs.io/en/latest/)
- [YARR Repository](https://gitlab.cern.ch/YARR/YARR/)
- [Local DB Tools Repository](https://gitlab.cern.ch/YARR/localdb-tools)

## Flow

In DB demonstration, we can do as follow things:

1. pre requirements<br>
Install the requirements for DB demonstration<br>
(Python3 and packages, MongoDB, influxDB, Viewer, YARR SW, DB Tools...)
    - [For centOS](database_demonstration_setup_centos.md)

<!--    
    - [For macOS](database_demonstration_setup_mac.md)
    - [For Ubuntu](database_demonstration_setup_ubuntu.md)
    - [For Windows](database_demonstration_setup_windows.md)
-->

2. Set-up
    - [MongoDB(on DB mahine)](database_demonstration_mongodb.md)
    - [influxDB(on DB mahine)](database_demonstration_influxdb.md)
    - [Grafana(on your browser)](database_demonstration_grafana.md)
    - [Viewer Application(on DB machine and on your browser)](database_demonstration_viewer.md)
    - [YARR SW for Local DB(DAQ machine)](database_demonstration_yarr.md)
<!-- 3. [Module Registration](database_demonstration_register_itkpd.md)<br>
This is not followed in this tutorial.-->

3. [Module Download(on your browser)](database_demonstration_download_itkpd.md)<br>
Download the module data into Local DB from ITkPD.
4. [Run DCS controller and checking DCS data in Grafana](database_demonstration_run_dcs.md)<br>
Run DCS controller and checking them in Grafana
5. [scanConsole & Upload](database_demonstration_scanconsole.md)<br>
Run scanConsole with uploading the test data into Local DB
6. [Viewer Application](database_demonstration_check_viewer.md)<br>
Check the uploaded data in the Viewer Application
7. [Select and Upload results into ITkPD](database_demonstration_upload_itkpd.md)<br>
Upload the test data into ITkPD (if possible)

<!--
![demo flow](images/demo_flow.png)
-->
