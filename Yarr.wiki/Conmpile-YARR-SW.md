# Ready

## 1) Git clone 
```
$ git clone https://github.com/jlab-hep/Yarr.git
$ cd Yarr
```
## 2) Choose DB on YARR SW version
```
$ git checkout database-devel
```

## 3) Load mongocxx and boost libraries
```
$ source /opt/rh/rh-mongodb36/enable
```

## 4) Use Makefile to compile
```
$ cd src
$ scl enable devtoolset-7 bash 
$ make -j4
```

Wait a couple of minutes. If there is no error occurred, It succeed!

# Usage
   Check [Quick tutorial for Yarr](https://github.com/jlab-hep/Yarr/wiki/Quick-tutorial-for-Yarr)