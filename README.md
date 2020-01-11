# PyArmor Server

This is a simple webserver for PyArmor WebUI.

Start a web server on local port 9096 and open web browser:

    python server.py

Start on other port 8089:

    python server.py -p 8089

Start without opening web browser:

    python server.py -n

## API

* /version

Get version information of PyArmor, Server and Python

URL

    http://localhost/version

Method: POST

Arguments: No

Success: HTTP/1.1 200 OK

Return

| Name       | Type    | Required | Length | Description |
|------------|---------|----------|--------|-------------|
| version    | String  |    Y     |        | PyArmor version |
| regcode    | String  |          |        | PyArmor registration code, empty for trial version |
| reginfo    | String  |          |        | PyArmor registration name and email |
| server     | String  |          |        | PyArmor Server version |
| python     | String  |          |        | Python version |

For example

    {
    "version": "5.9.0",
    "regcode": "pyarmor-vax-00001",
    "reginfo": "jondy (jondy.zhao@*****.com)",
    "server": "0.1",
    "python": "3.7.0",
    }

Error: HTTP/1.1 400 Bad Request

For example

    {
    "username": ["A user with that username already exists."]
    }

* /directory/list

List directories and files in this path

URL

    http://localhost/directory/list

Method: POST

Arguments

| Name       | Type    | Required | Length | Description |
|------------|---------|----------|--------|-------------|
| path       | String  |    Y     |        | '@', '', '/', '/Users/jondy' |
| pattern    | String  |          |        | '*.py', filter the result files |

If path is `@`, return some favorite pathes, for example, User home
path, My Documents etc.

If path is empty, list the current path of PyArmor Server

Success: HTTP/1.1 200 OK

Return

| Name       | Type    | Required | Length | Description |
|------------|---------|----------|--------|-------------|
| path       | String  |    Y     |        | Absolute path of request path |
| dirs       | List    |    Y     |        | All the directories in this path |
| files      | List    |    Y     |        | All the files matched the pattern in this path |

The list of `dirs` and `files` are sorted ignore case sensitivity.

For example

    {
      "path": "/Users/jondy",
      "dirs": [ "Desktop", "workspace" ],
      "files": []
    }
    
* /directory/new

Make a directory

URL

    http://localhost/directory/new

Method: POST

Arguments: String, path to create

Success: HTTP/1.1 200 OK

Return: Absolute path created

* /directory/remove

Remove a directory

URL

    http://localhost/directory/remove

Method: POST

Arguments: String, path to remove

Success: HTTP/1.1 200 OK

Return: Absolute path removed

* /project/list

* /project/new

* /project/update

* /project/remove

* /project/build

* /project/build_temp

* /license/list

* /license/new

* /license/update

* /license/remove

* /runtime/list

* /runtime/new

* /runtime/update

* /runtime/remove
