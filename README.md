## iftttest

CLI client to simulate IFTTT Channel interaction.

Not publicly distributed through npm at this time.

### Configure your channel

Set channel options with the `set` command.

Setting the `host` is required before running other commands. If no protocol is given, `http://` is assumed.

To set the `host`:

```bash
iftttest set host localhost:8000
```

To set a client `secret` (optional):

```bash
iftttest set secret my-special-client-secret
```

Print the current channel options to the console with the `config` command:

```bash
iftttest config
```

### Usage

```bash
iftttest COMMAND [OPTIONS]
```

To run a status check against a channel:

```bash
iftttest status
```

Or to simulate a trigger check:

```bash
iftttest trigger -t my-trigger
```

### Output

You'll see the request's HTTP method, the URL, and any submitted JSON body. Then, the response's status code, and body.

Running `iftttest status` would get you output like:

```
GET: http://localhost:8000/ifttt/v1/status
Status: 200

{
    "data": {
        "status": "OK",
        "time": "2014-02-01T19:33:04.932Z",
        "message": "Everything is A-oh-fine."
    }
}
```

Running `iftttest trigger -t new-terrific-updates` would you get output like:

```
POST: http://localhost:8000/ifttt/v1/triggers/new-terrific-updates
With: {}
Status: 200

{
    "data": [
        {
            "ifttt": {
                "id": "terrific-123",
                "timestamp": "2014-01-24T00:00:00Z"
            },
            "TerrificMessage": "Everything is so terrific!"
        }
    ]
}
```

### Not yet supported

Lots of things!

* Trigger fields
* Dynamic trigger options
* Dynamic trigger validation
* User authentication
* User information
* Channel actions

And useful ideas:

* Allow validation of responses (e.g. complies with IFTTT API?)
* "Pipe mode", where the only STDOUT output is response JSON
* help command per-command, to show options for `trigger`, etc.