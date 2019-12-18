# Viewer Application

## Goal

Check the Web Page on your browser.

![Viewer Application Goal](images/demo_viewer_goal.png)

## Pre Requirements

Viewer Application is implemented in "Local DB Tools".<br>
You can install "Local DB Tools" as follows:

```bash
$ git clone -b devel https://gitlab.cern.ch/YARR/localdb-tools.git
```

## Getting start

### 1. Setup Viewer Application by the script 'set_viewer.sh'

In this step, you have to set the editor command (e.g. vim, emacs) if the environmental variable 'EDITOR' has not registered.

```bash
$ cd localdb-tools/viewer
$ ./set_viewer.sh
[LDB] Set editor command ... > vim
[LDB]
[LDB] Welcome to Local Database Tools!
<some texts>
[LDB] More information: https://localdb-docs.readthedocs.io/en/master/
```

### 2. Start the application by the command 'app.py'

```bash
$ ./app.py --config conf.yml
INFO Viewer Application URL: http://127.0.0.1:5000/localdb/
 * Serving Flask app "app" (lazy loading)
 * Environment: production
```

### 3. Access the Web Page

Access to [http://127.0.0.1:5000/localdb/](http://127.0.0.1:5000/localdb/) on the machine's browser where app.py is running,<br>
and you can see the web page as follows:

![viewer top](images/demo_viewer_top.png)

Finish!

## More Detail

Check [Viewer Application Page](viewer.md) for more detail.
