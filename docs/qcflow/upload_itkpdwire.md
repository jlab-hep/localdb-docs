[Tutorial's Top page](flow.md)<br>
[Previous step](signoffwire.md)<br>
<hr>

# Upload selected results to ITkPD

You can upload selected QC test results to ITkPD.<br>
Please follow the instruction below after sign-in on your viewer to click "Sign-in" at the top left conner.<br>
![Upload_Results_To_ITkPD](../images/qc-flow/upload_results_itkpd.png)<br>

You can check the resutls at web page for ITkPD:

[https://itkpd-test.unicorncollege.cz/myTests](https://itkpd-test.unicorncollege.cz/myTests)


At Wirebonding, we will upload results for Pixel Failure Tests(Full Electrical Tests). So LocalDB will attach scan config files to a module:
![scan_config](../images/qc-flow/scan_configs.png)
### Config Zip: `BestCfg_<temp>_degree_<stage_name>.zip`
- Chip config files (json file)

We developed a tool to download `BestCfg_<temp>_degree_<stage_name>.zip` from ITkPD: [Git](https://gitlab.cern.ch/hirose/ModuleConfigDownloader)<br>
Using config files, we can upload scan results for a module at the reception site.


<br>
Next, I show how to download QC-test results from ITkPD.

Go to next step.<br>
[Pull the list of QC test results from ITkPD](download_results.md)<br>
