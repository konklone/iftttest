## iftttest

CLI client to simulate IFTTT Channel interaction.

Not publicly distributed through npm at this time.

### Usage

```bash
iftttest HOST COMMAND [OPTIONS]
```

Where `HOST` is the base hostname of the channel, e.g. `localhost:8000`. If no protocol is given, `http://` is assumed.

To run a status check against a channel running at `localhost:8000`:

```bash
iftttest localhost:8000 status
```

Or to simulate a trigger check:

```bash
iftttest localhost:8000 trigger -t my-trigger
```

### Output

You'll see the request's HTTP method, the URL, and any submitted JSON body. Then, the response's status code, and body.

Running `iftttest localhost:8000 status` would get you output like:

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

Running `iftttest localhost:8000 trigger -t new-terrific-updates` would you get output like:

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

* User authentication
* User information
* Shared secrets
* Trigger fields
* Dynamic trigger options
* Dynamic trigger validation
* Channel actions

And useful ideas:

* Allow validation of responses (e.g. complies with IFTTT API?)
* If no command, assume command `status`
* If no command but a `-t` option is given, assume command `trigger`
* Check for default host in a `$HOME/.iftttest` file
* "Pipe mode", where the only STDOUT output is response JSON