[Tutorial's Top page](flow.md)<br>
[Previous step](signoffwire.md)<br>
<hr>

You can upload selected QC test results to ITkPD.<br>
Please follow the instruction below after sign-in on your viewer to click "Sign-in" at the top left conner.<br>
![Upload_Results_To_ITkPD](../images/qc-flow/upload_results_itkpd.png)<br>

You can check the resutls at web page for ITkPD:

[https://itkpd-test.unicorncollege.cz/myTests](https://itkpd-test.unicorncollege.cz/myTests)


After uploading the results, we will start QC test for Wirebonding.


At Wirebonding, we will upload results for Pixel Failure Tests(Full Electrical Tests). So LocalDB will attach scan config files to a module:
![scan_config](../images/qc-flow/scan_configs.png)
- Config Zip: `BestCfg_<temp>_degree_<stage_name>.zip`
  - Visual Inspection
  - Wirebond info
  - Wirebond pull test
  - Sensor IV
  - SLDO VI
  - Pixel Failure Test (Full Electrical Test)

We developed a tool to download `BestCfg_<temp>_degree_<stage_name>.zip` from ITkPD: [Git](https://gitlab.cern.ch/hirose/ModuleConfigDownloader)

<br>
Next, I show how to download QC-test results from ITkPD.

Go to next step.<br>
[Pull the list of QC test results from ITkPD](download_itkpd.md)<br>
