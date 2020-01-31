# Database Demonstration

## Tutorial Flow
~~~explanation

In DB demonstration, we can do as follow things:
### Installation and setup for DB machine
~~~explanation
- [Installation](database_demonstration_install_db_machine.md)
- [Setting for MongoDB](database_demonstration_mongodb.md)
- [Setting for LocalDB viewer](database_demonstration_viewer.md)

### Installation and setup for DAQ machine
~~~explanation
- [Installation](database_demonstration_install_daq_machine.md)
- [Setup YARR SW for LocalDB](database_demonstration_yarr.md)

### QC Flow
3. [Module Download](database_demonstration_download_itkpd.md)<br>
Download the module data into Local DB from ITkPD.
4. [Run DCS controller](database_demonstration_run_dcs.md)<br>
Run DCS controller and get values(environment temp,current,voltage)
5. [Grafana](database_demonstration_grafana.md)
Checking the data in Grafana
6. [scanConsole](database_demonstration_scanconsole.md)<br>
Run scanConsole with storing the test data into Local DB
7. [Viewer Application](database_demonstration_check_viewer.md)<br>
Check the uploaded data in the Viewer Application
8. [Select and Upload results into ITkPD](database_demonstration_upload_itkpd.md)<br>
Upload the test data into ITkPD (if possible)

<!--
![demo flow](images/demo_flow.png)
-->
