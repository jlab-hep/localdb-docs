# Site Config

You can specify the configuration of the production site when uploading data into Local DB.

#### File Format

Site configuration file uses the JSON format:

```json
{
    "institution": "PRODUCTION SITE"
}
```

If the institution is registered in ITk PD, you can specify the institution using "code":

```json
{
    "code": "INSTITUTION CODE"
}
```

#### Options

- `institution`<br>
_Type_ : string<br>
_Default_ : HOSTNAME (an environmental variable on UNIX system specifying the hostname)<br>
Specifies the name of the production site or institution. (e.g. "ABC Laboratory")

- `code`<br>
_Type_ : string<br>
Specifies the institution code defined in ITk PD.
