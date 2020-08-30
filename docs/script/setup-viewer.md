# setup_viewer.sh

This is a script for setting the configuration of the [viewer application](../viewer.md) and installing some tools to display plots on web browser.<br>
This script creates the [viewer config file](../config/viewer.md), and you can start the viewer application with it.

- Location: `localdb-tools/viewer/setup_viewer.sh`
- Syntax:

```bash
$ cd localdb-tools/viewer
$ ./setup_viewer.sh [-i address]
                    [-p port]
                    [-c name]
```

### Flow

1. Check the [required packages](../installation/requirements-list.md)
2. Check the configuration of Local DB server
    - Display the configuration
    - Prompt for confirmatio (Proceed if y or exit if n)
3. Check whether to enable admin function
    - Prompt for confirmation (Proceed if y or skip if n)
    - User autorization (Proceed on success, or exit on failure)
4. Create config file (admin_conf.yml if the admin function is enabled, or user_conf.yml if not disabled)
5. Install and compile the [plotting tool](https://gitlab.cern.ch/YARR/utilities/plotting-tools) for displaying plots on the viewer
6. Install and compile the [analysis tool](https://gitlab.cern.ch/hokuyama/analysis-tool) for analysing the electrical tests on the viewer

### Usage

```bash
$ cd localdb-tools/viewer
$ ./setup_viewer.sh
[LDB] Welcome to Local Database Tools!
[LDB] Check python modules...
[LDB] Requirements already satisfied
[LDB]
Local DB Server IP address: 127.0.0.1
Local DB Server port: 27017

[LDB] Are you sure thats correct? [y/n]
> y
...
```

This script first checks that you have the required packages.<br>
The output of **Requirements already satisfied** means that the confirmation is successful.<br>
If you get an error, follow [FAQ for Viewer](../faq/viewer.md) to resolve it.

The script displays the configuration of Local DB server.<br>
You need to check it and answer **y** to proceed, or **n** to exit.

```bash
...
[LDB] Are you sure thats correct? [y/n]
> y

[LDB] Do you use admin functions for LocalDB viewer? [y/n]
> y

Input localDB admins username: username
Input localDB admins password: password

[LDB] Authentication succeeded!
...
```

The script next checks whether to enable administrator functions.<br>
See the [admin functions in the viewer](../viewer.md) to get more about what you can do.<br>

If you want to enable the admin functions, you need to [create an admin account in Local DB by create_admin.sh](create_admin.md).<br>
Once you have created the admin account, you can answer **y** to proceed and enter the username and password of the admin account to authenticate.<br>

If you do not need to enable the admin functions, you can answer **n** and skip the steps.

**RECOMMEND**<br>
**It is recommended to create an admin account and lock MongoDB of Local DB to protect data.**

```bash
...
[LDB] Setting the configuration file: /home/example/localdb-tools/viewer/admin_conf.yml
...
```

The script creates the config file for the viewer application in `localdb-tools/viewer/admin_conf.yml` if you enable the admin functions or in `localdb-tools/viewer/user_conf.yml` if not.

```bash
...
[LDB] Check plotting tool and analysis tool...
...
```

The script install the [plotting tool](https://gitlab.cern.ch/YARR/utilities/plotting-tools) for displaying plots on the viewer, and the [analysis tool](https://gitlab.cern.ch/hokuyama/analysis-tool) for analysing the electrical tests on the viewer, and compile them if the ROOT function is available.<br>
If you have not enable the ROOT function, you can enable it by `source path/to/where/ROOT/installed/bin/thisroot.sh`, or the script skip the steps automatically if the ROOT is disabled.

```bash
...
[LDB] Finished setting up of Viewer Application!!
[LDB]
[LDB] Start Viewer Application by ...
[LDB]   python3 app.py --config admin_conf.yml &
[LDB]
[LDB] Access the Local DB page on web browser ...
[LDB]   http://localhost:5000/localdb/
[LDB]
[LDB] More information: https://localdb-docs.readthedocs.io/en/devel/
```

The output of **Finished setting up of Viewer Application!!** means that the setup is successful, and you can run the viewer application:

```bash
$ ./app.py --config admin_conf.yml
```

or

```bash
$ ./app.py --config user_conf.yml
```

See the [viewer application](../viewer.md) to get more usage.

### Additional options

```bash
$ ./setup_viewer.sh -h

Make the config file and setup for the viewer application by:

    ./setup_viewer.sh [-i ip address] [-p port] [-c config]

Options:
    - i <IP address>  Local DB server IP address (default: 127.0.0.1)
    - p <port>        Local DB server port (default: 27017)
    - c <config>      Config file name (default: user_conf.yml or admin_conf.yml)
```
