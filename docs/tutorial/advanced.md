# Advanced Tutorial

- c. [Register component data into Local DB from ITk PD (ITkPD Interface)](#c-register-component-from-itkpd)
- d. [Scan and Upload data associated with the component data into Local DB](#d-upload-test-data)
- e. [Register DCS data associated with the test data](#e-register-dcs)
- f. [Share data with the other Local DB (Synchronization Tool)](#f-share-data)
- g. [Back-up Local DB (Archive Tool)](#g-backup)

## c. Register Component from ITkPD

You can download component information from ITk production database and register the info to Local DB.<br>

```bash
# 1. Set
$ cd <YOUR_WORK_DIRECTRY>
$ cd localdb-tools
$ cd itkpd-interface
$ ./setup_interface_tool.sh

# 2. Login ITk production database
$ source authenticate.sh
Input Access Code 1 for ITkPD:<input your access code 1 for ITkPD>
Input Access Code 2 for ITkPD:<input your access code 2 for ITkPD>
[2019-12-27 16:05:33,138][WARNING           ]  Saved user session is expired in .auth. Creating a new one. (core.py:55)
You have signed in as <username>. Your token expires in 7197s.

# 3. Download compontnent info
$ ./bin/downloader.py --config my_conf.yml --option Module
2019-12-27 16:08:51 <hostname> <username>[2856] INFO [LDB] Found <# of component> module(s)! Start downloading...
...
2019-12-27 16:08:51 <hostname> <username>[2856] INFO [LDB] Finished!!
```

You can check the downloaded components on the url:'http://127.0.0.1:5000/localdb/component' or corresponded url on the local browser in Local DB.

## f. Share Data

You can share data with other Local DB using Synchronization Tool.<br>
Please check [the detail page](../tool/sync.md) to get how to use.

## g. Backup

You can keep the back-up of Local DB using Archive Tool. <br>
Please check [the detail page](../tool/archive.md) to get how to use.

