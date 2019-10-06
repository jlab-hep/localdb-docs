# Version of DB on YARR SW
There is 3 versions of DB on YARR SW by ASIC types.
* tag: "db-v0.8" for both of RD53A and FEI4B with sw (Yarr: d412eaf9)
* tag: "old-db-v" for RD53A with old-sw (Yarr: 0f968b5f)
* tag: "old-sw-old-db-v" for FEI4B with old-sw (Yarr: 7c4a0727)

# Ready

## 1) Git clone 
```
$ git clone https://github.com/jlab-hep/Yarr.git
$ cd Yarr
```
## 2) Choose DB on YARR SW version

* For latest version of DB SW + YARR

  ```
  $ git checkout -b tag-db-08 db-v0.8
  ```

* For RD53A

  ```
  $ git checkout -b tag-old-db refs/tags/old-db-v
  ```

* For FEI4B

  ```
  $ git checkout -b tag-old-sw-old-db refs/tags/old-sw-old-db-v
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


***


In [database branch](https://github.com/jlab-hep/Yarr), we added boost and mongocxx-v3's header files path and libraries path.

* Header files path

  [Makefile l.38](https://github.com/jlab-hep/Yarr/blob/6dcbb3b362369a42cd13a47ea06c8b0ccff792d3/src/Makefile#L38)
  ```
  CPPFLAGS += -I/opt/rh/rh-mongodb36/root/usr/include/mongocxx/v_noabi -I/opt/rh/rh-mongodb36/root/usr/include/bsoncxx/v_noabi
  ```

* Libraries path

  [Makefile l.39](https://github.com/jlab-hep/Yarr/blob/6dcbb3b362369a42cd13a47ea06c8b0ccff792d3/src/Makefile#L39)
  ```
  LDFLAGS += -L/opt/rh/rh-mongodb36/root/usr/lib64 -lmongocxx -lbsoncxx
  ```

# Usage
   Check [Quick tutorial for Yarr](https://github.com/jlab-hep/Yarr/wiki/Quick-tutorial-for-Yarr)