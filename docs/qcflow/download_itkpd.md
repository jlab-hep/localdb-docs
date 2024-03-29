# Download the module ID infos from the Production DB

### Download component information from Production DB
Download the component data from Production DB.<br>

Go to the downloading page [http://127.0.0.1:5000/localdb/download_component](http://127.0.0.1:5000/localdb/download_component)<br><br>

**Input LocalDB admin's username and password for "Authentication Required".**<br>
**Basically, admin only can go to this page and use the interfacing functions between prodDB and LocalDB.**<br><br>


Follow the instruction bellow to download module from prodDB:
![download from itkpd](../images/qc-flow/download_component_from_itkpd.png)
![prodDB account](../images/qc-flow/database_prodDB_account.png)

You can check the downloaded component data using Viewer Application.<br>
Check [http://127.0.0.1:5000/localdb/components](http://127.0.0.1:5000/localdb/components) on your browser,<br>
and you can find the components with ATLAS serial numbers.<br><br>

We use an RD53A module's property in this tutorial.<br>
The device's serial number is "20UPGRS0000009" or "20UPGRS0000010", the chip's serial number is "20UPGRA0000026" or "20UPGRA0000027". Check the information in the viewer.<br><br>

![demo_download_module](../images/qc-flow/demo_download_module.png)

Go to next step.<br>
[Hook-up the module to the devices and Run the DCS controller](run_dcs.md)<br>
