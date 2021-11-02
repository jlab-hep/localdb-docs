[Tutorial's Top page](flow.md)<br>
[Previous step](register_module.md)<br>
<hr>

# Upload QC-test results for Bare to PCB

## Test Items for Bare to PCB

![demo scan](../images/qc-flow/stage_bare.png)

- Bare to PCB
  - Visual Inspection
  - Metrology (<span style="color: red; ">Old format</span>)
  - Mass
  - Glue Flex Attach infomation



## QC-helper
QCHelper is GUI to upload QC results to localDB.

![demo scan](../images/qc-flow/QCHepler_structure.png)

### 1. Start GUI

```bash
$ cd Workdir/qc-helper
$ python3 main.py
```
<br>

### 2. Operating procedure

Please follow "instruction.pdf" in the latest version of the [QCHelper](https://gitlab.cern.ch/atlas-itk/sw/db/pixels/qc-viz-tools-dev/qc-helper/-/tree/master/doc/Instruction)

<br>

### 3. Check the uploaded results in LocalDB viewer

Open your browser and access the LocalDB viewer.
The url is [http://127.0.0.1:5000/localdb](http://127.0.0.1:5000/localdb) or https://IPADRESS:5000/localdb.

#### Go to the module's toppage following the instruction below.
![demo scan](../images/qc-flow/goto_module_toppage.png)

You can see the uploaded results in the table of "QC Test" in the page as below.
You can go to the result page for each test by clicking the ids in the table.

![demo scan](../images/qc-flow/check_results_localdb.png)

After uploading all required test results to LocalDB, we can proceed a stage.

Go to next step.<br>
[Sign-off each stage](signoffbare.md)<br>