# 1. Introduction

The **viewer** is display the contents in Local DB on web browser. <br>
You can access the web page in the local machine, or from the other machine by opneing port or using apache service.

# 2. Getting start

Please look at [Installation/Set-up Viewer Application](install.md) to set-up Viewer Application.

# 3. Usage

```bash
$ cd localdb-tools/viewer
$ ./app.py --config conf.yml 

Applying ATLAS style settings...

 * Serving Flask app "app" (lazy loading)
 * Environment: production
   WARNING: Do not use the development server in a production environment.
   Use a production WSGI server instead.
 * Debug mode: off
2019-10-09 12:37:46 lazulite werkzeug[1991] INFO  * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

**Command Line Arguments**

- `--config` : path to configure file

# 4. Web Page

Please access `http://127.0.0.1:5000/localdb/` on web browser in local machine and it displays the following page:

**Top Page**

|![Viewer Top Page](images/viewer_top.png)|
|:-:|

**Component List Page**

|![Viewer Component Top Page](images/viewer_top_component.png)|
|:-:|

**Test List Page**

|![Viewer Test Top Page](images/viewer_top_test.png)|
|:-:|

You can access the test result page by clicking 'result page', and it displays the following page:

|![Viewer Result Page](images/viewer_result.png)|
|:-:|

# 5. Remote Access/Apache

In edit.

