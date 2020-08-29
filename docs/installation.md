# Installation

You need to install the [requirements for the system](requirements-list.md) on your computer.<br>
The Local DB System is supporting **centOS7** and **macOS** currently.<br>
Before proceeding to install, clone git repository of [YARR](https://gitlab.cern.ch/YARR/YARR) and [Local DB Tools](https://gitlab.cern.ch/YARR/localdb-tools):

```bash
$ cd <YOUR_WORK DIRECTRY>
$ git clone https://gitlab.cern.ch/YARR/YARR.git
$ git clone https://gitlab.cern.ch/YARR/localdb-tools.git
```

!!! Warning
    Some Local DB functions are not available yet in master buranch.<br>
    Please change to devel branch if want to use.

## Installation for centOS7

- [Manual Installation (**RECOMMENDED**)](manual-install.md)
- [Automatic Installation](automatic-install.md)

## Installation for macOS

- [Manual Installation (**RECOMMENDED**)](manual-install-macos.md)
- [Automatic Installation](automatic-install-macos.md)

Once installed the required packages, you can try it out following the [tutorial page](tutorial.md).<br>
See the [manual page for each tool](tool.md) to get the individual functions.
