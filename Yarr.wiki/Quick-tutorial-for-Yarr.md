This page describes how to upload data into database after scan in YARR.

## 1) Ready

### Add environment info
Change `Yarr/src/configs/testRunInfo.json` as test environment.
It looks like below :
```
{
   "assembly": {
        "stage": "encapsulation",              # assembly stage of this module
        "userIdentity": "FirstName_LastName",  # shifter's name
        "institution": "Abc_University"        # shifter's institution
   },
   "environments": [
        {
           "key": "lv",                        # key word of the environment item
           "value": "1.8",                     # value
           "description": "Low voltage [V]"    # description + unit
        },
        {
           "key": "lv_current",
           "value": "1.0",
           "description": "Low voltage current [A]"
        }
   ]
}
```

## 2) Do scan
  * [For FE-I4B](https://github.com/jlab-hep/Yarr/wiki/fei4b-quad)
  * [For RD53A](https://github.com/jlabhep/Yarr/wiki/rd53a)