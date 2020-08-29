# Viewer Tutorial

This tutorial describes the oprations related to [viewer](viewer.md) setup and some browser functions.

!!! Recommend
    If you have not uploaded any data into Local DB yet, it is recommended to see the [basic tutorial](basic-tutorial.md) and upload scan data before proceeding with this page.

### Table of Contents

1. [How to Setup Viewer Application](#4-how-to-setup-viewer)
2. [How to Check Data in Viewer Application](#5-how-to-check-data-in-viewer)

---

## 1. How to Setup Viewer

#### Setup configuration

Change the directory where you have cloned [Local DB Tools](https://gitlab.cern.ch/YARR/localdb-tools):

```bash
$ cd path/to/localdb-tools
```

And load path to ROOT installed directory to enable the plotting function in the viewer application:

```bash
$ source path/to/root/bin/thisroot.sh
```

First make sure to setup the configuration files of the [viewer application](viewer.md) using [localdb-tools/viewer/setup_viewer.sh](setup-viewer.md) script:

```bash
$ cd viewer
$ ./setup_viewer.sh
```

This script checks missing python packages, prepares default config files, install some useful functions using git.

```bash
### script output
Local DB Server IP address: 127.0.0.1
Local DB Server port: 27017

[LDB] Are you sure that's correct? [y/n]
> y
```

Answer **y** to proceed if you did not change any settings when you installed MongoDB.<br>

```bash
### script output
[LDB] Do you use admin functions for LocalDB viewer? [y/n]
> n
```

Answer **n** to proceed.

!!! Note
    Once you enable the administrator function, you can use various functions in the viewer application.<br>
    In this tutorial, you will skip that step and proceed next.<br>
    See [what can be done with the admin function and how to set it] to get more information.<br>

This script creates the [viewer config file](viewer-config.md).

#### Run application

Run python script to start the [viewer application](viewer.md) on the local host machine:

```bash
$ python3 app.py --config user_conf.yml
2020-08-27 15:28:09 guest0 root[29905] INFO [LDB] Viewer Application URL: http://127.0.0.1:5000/localdb/
 * Serving Flask app "app" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
2020-08-27 15:28:09 guest0 werkzeug[29905] INFO  * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

You can access the Local DB viewer on the local browser while this application is running.<br>

## 2. How to Check Data in Viewer

#### Top Page

Access [http://127.0.0.1:5000/localdb/](http://127.0.0.1:5000/localdb/) on the local browser:

|![Viewer Top Page](images/viewer_top.png)|
|:-:|

<br>

#### Scan List Page

Click **Scan Page** to switch to the scan list page:

|![Viewer Test Top Page](images/viewer_top_test.png)|
|:-:|

<br>

#### Scan Result Page

Click **result page** to switch the scan result page:

|![Viewer Result Page](images/viewer_result.png)|
|:-:|

<br>
