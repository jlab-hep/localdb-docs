## User Config

You can specify the configuration of your user account when uploading data into Local DB.

### File Format

User configuration file uses the JSON format:

```json
{
    "userName": "FIRSTNAME LASTNAME",
    "institution": "YOUR INSTITUTION",
    "description": "default"
}
```

If you have your account in Local DB Viewer, you can specify your user account using "viewerUser":

```json
{
    "viewerUser": "username"
}
```

### Core Options

- `userName`<br>
_Type_ : string<br>
_Default_ : USER (an environmental variable on UNIX system specifying your user account)<br>
Specifies your name (e.g. "John Doe").

- `institution`<br>
_Type_ : string<br>
_Default_ : HOSTNAME (an environmental variable on UNIX system specifying the hostname)<br>
Specifies the name of the institution you belong to. (e.g. "ABC Laboratory")

- `description`<br>
_Type_ : string<br>
_Default_ : "default"<br>
Add descriptions for the user account (e.g. "account for testbeam")<br>
If this is not specified, specifies "default", or "viewer" if "viewerUser" is specified.

- `viewerUser`<br>
_Type_ : string<br>
Specifies the name of your user account in Local DB Viewer.
