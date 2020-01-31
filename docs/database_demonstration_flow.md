# Database Demonstration

## Tutorial Flow
~~~explanation

In DB demonstration, we can do as follow things:
### Installation for DB machine
~~~explanation<br>
1. [Installation](database_demonstration_install_db_machine.md)<br>
2. [Setting for MongoDB](database_demonstration_mongodb.md)<br>
3. [Setting for LocalDB viewer](database_demonstration_viewer.md)<br>

### Installation for DAQ machine
~~~explanation<br>
1. [Installation](database_demonstration_install_daq_machine.md)<br>

### QC Flow
1. [Module Download](database_demonstration_download_itkpd.md)<br>
Download the module data into Local DB from ITkPD.
2. [Run DCS controller](database_demonstration_run_dcs.md)<br>
Run DCS controller and get values(environment temp,current,voltage)
3. [Check DCS data Grafana](database_demonstration_grafana.md)<br>
Checking the data in Grafana
4. [scanConsole](database_demonstration_scanconsole.md)<br>
Run scanConsole with storing the test data into Local DB
5. [Viewer Application](database_demonstration_check_viewer.md)<br>
Check the uploaded data in the Viewer Application
6. [Select and Upload results into ITkPD](database_demonstration_upload_itkpd.md)<br>
Upload the test data into ITkPD

<!--
![demo flow](images/demo_flow.png)
-->
