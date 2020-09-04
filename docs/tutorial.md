# Tutorials

This page introduces tutorials to try out the Local DB and its tools assuming some cases.<br>
If you want to try a series of operations from scan to data upload, go to the [scan tutorial](#scan-tutorial).<br>
If you want to try the operation related to the [viewer application](tool/viewer.md), go to the [viewer tutorial](#viewer-tutorial).<br>
If you could not complete the [installation](installation.md) or cannot build YARR and cannot use read-out binary command, go to the [trial tutorial](#trial-tutorial) to try starting Local DB and using the commands.<br>
If you want to check other advanced usage, go to the [advanced tutorial](#advanced-tutorial).

!!! Warning
    Current supported OS is centOS7 & macOS (greather than 10.14).<br>
    Let's try it on VM if your PC is neither.

---

## Basic Tutorials

### [Trial Tutorial](tutorial/trial.md)

Assuming you do not have root privileges and can not complete the [installation of the requirements](installation.md), this tutorial describes;

- How to build environment in user directory
- How to download a sample dataset and setup Local DB
- How to use read-out command and data upload without actually performing read-out test using a toy script

Once you have started Local DB in this trial tutorial, you can go to the [tutorial for the viewer application](tutorial/viewer.md) and try it out.

##### [Go to the trial tutorial page](tutorial/trial.md)

---

### [Scan Tutorial](tutorial/scan.md)

This tutorial is intended to demonstrate basic scan operations:

- How to build YARR read-out command
- How to use read-out command and data upload using emulator
- How to retrieve data from Local DB on the console

Once you have started Local DB in this trial tutorial, you can go to the [tutorial for the viewer application](tutorial/viewer.md) and try it out.

##### [Go to the scan tutorial page](tutorial/scan.md)

---

### [Viewer Tutorial](tutorial/viewer.md)

This tutorial is intended to demonstrate the operations related to [viewer application](tool/viewer.md):

- How to setup and start viewer application
- How to check data stored in Local DB on local browser
- How to use administrator functions on viewer application

If you have not tried the function of uploading test data into Local DB and you do not have data in Local DB, go to the [scan tutorial](tutorial/scan.md) and upload scan data before proceeding this tutorial.

##### [Go to the viewer tutorial page](tutorial/viewer.md)

---

## Advanced Tutorials

### [DCS Tutorial](tutorial/dcs.md)

### [Component Tutorial](tutorial/component.md)

### [Synchronization Tutorial](tutorial/sync.md)

### [Archiving Tutorial](tutorial/archive.md)

<!--TODO


This is an advanced instruction for using Local DB and Tools.<br>

#### Table of Contents

- a. Setup Web application of Local DB (Viewer Application)
- b. Register component data into Local DB
- c. Retrieve component data from ITkPD into Local DB (ITkPD Interface)
- d. Scan and Upload data associated with the component data into Local DB
- e. Register DCS data associated with the test data
- f. Share data with the other Local DB (Synchronization Tool)
- g. Back-up Local DB (Archive Tool)

##### [Go to the advanced tutorial page](tutorial/advanced.md)
-->
