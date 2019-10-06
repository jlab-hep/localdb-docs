This page describes how to check data in database via web interface.

## 0) Configuration file

1) Change `web-app-db-yarr/conf.yml` as your setup. 

   It looks like below :
   ```
   mongoDB:
     host: 127.0.0.1 # IP address where mongodb running
     port: 27017     # port of mongodb
     db: yarrdb
     userdb: userdb
 
   # For user authentication
   #username: viewer
   #password: viewerpass

   flask:
     host: 127.0.0.1 # IP address where the viewer running
     port: 5000      # port of the viewer
 
   # For summary.py
   summary:
     serial: AA-11        # serial number of module to add summary
     stage: encapsulation # stage to add summary
 
   python: 2         # version of python you use
   ```


## 1) Start a web server
```
$ cd path/to/web-app-db-yarr 
$ python app.py --config conf.yml

* Serving Flask app "app" (lazy loading)
* Running on http://127.0.0.1:5000/
```
> type "127.0.0.1:5000/yarrdb/" in browser to check the viewer <br>
> also type "127.0.0.1/yarrdb/" is avalable to check after starting apache system (ref : [installation](https://github.com/jlab-hep/Yarr/wiki/Web-interface)/Advance)