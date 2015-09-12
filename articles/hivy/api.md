---
sidebar_current: "hivy-api"
---

# Hivy API


## Token

TODO

## Status and documentation

```console
$ curl http://0.0.0.0:5000
{
  "state": {
    "hivy": true,
    "sub-systems": {
      "consul": {
        "leader": "192.168.0.19:8300",
        "peers": [
          "192.168.0.19:8300"
        ]
      },
      "docker": true,
      "salt-master": false
    }
  },
  "version": {
    "consul_": "not implemented",
    "docker": {
      "ApiVersion": "1.10",
      "Arch": "amd64",
      "GitCommit": "dc9c28f",
      "GoVersion": "go1.2.1",
      "KernelVersion": "3.11.0-20-generic",
      "Os": "linux",
      "Version": "0.10.0"
    },
    "hivy": {
      "major": 0,
      "minor": 0,
      "patch": 9
    },
    "salt": {
      "Jinja2": "2.7.2",
      "M2Crypto": "0.22",
      "PyYAML": "3.11",
      "PyZMQ": "14.2.0",
      "Python": "2.7.5 (default, Nov 30 2013, 10:53:27)",
      "Salt": "2014.1.3",
      "ZMQ": "2.2.0",
      "msgpack-pure": null,
      "msgpack-python": "0.4.2",
      "pycrypto": "2.6.1"
    }
  }
}
```

```console
$ curl http://0.0.0.0:5000/v0/doc
{
    "api": {
        "GET /": " Expose Hivy services states and versions ",
        "GET /v0/docs": " Expose last api documentation ",
        "GET /v0/nodes?where=localhost": " User nodes organization ",
        "GET | POST | PUT | DELETE /v0/nodes/<string:image>?where=localhost&user=dockerfile": " Container High level management ",
        "GET | POST | PUT | DELETE /v0/proxy/<string:frontend>?node=ghost&reset=True&name=blog": " Hipache High level management ",
        "GET | PUT /v0/users/<string:username>": " Register new users and inspect them "
    }
}
```


## Node lifecycle

### Default creation

The following command spins up a `base` image.

```console
$ curl -X POST -H "Authorization:$TEST_API_KEY" "http://0.0.0.0:5000/v0/node/base"
{
  "Id": "7becce0b8dec80c3f80b378c2ae41f0d9da1ab113d99c4537de8a0cd6e9a50a6",
  "Warnings": null,
  "name": "hivetech-base"
}
```

### More control

In addition to standard services (ssh, consul, salt, ...), we can specify
custom elements for our environment :

* Environment variable
* Serice dependencies
* Exposed ports

```console
$ curl -X POST \
  -H "Authorization:$TEST_API_KEY" \
  --data '{\
    "ports": [5000],\
    "env": {"QUANDL_API_KEY":"vebrzrzzr"},\
    "links": ["rethinkdb"]\
  }' \
  "http://0.0.0.0:5000/v0/node/base"
```

`ports` field will expose to public a virtual container port, mapping it to a
random one of the host (we can check which one inspecting the image state, see
below).

`links` deserves further explanations. *Hivy* waits for an array of container
names, like the ones we provide on creation. Then it will inject into the new
container some consistent environment variables our app can use to connect to
services.

```console
$ # Say we create a database first
$ curl -X POST ... http://.../node/rethinkdb?user=dockerfile
$ # Then we post an app using this database
$ curl -X POST ... \
  --data '{"links": ["rethinkdb"]}' \
  http://.../node/our-app
$ # It will inject into <user>/our-app container :
$ #   - RETHINKDB_HOST (like 172.17.0.3)
$ #   - RETHINKDB_PORTS_EXPOSED (like 28015,28014,8080)
$ #   - RETHINKDB_PORT_28015 (mapping of the official port)
$ #   - RETHINKDB_PORT_XXXXX (for each of exposed port)
```

By default, *Hivy* uses the username to complete the image name (like
`hivetech/base` above). However we can override this behavior to enjoy what
other talented developers packed into containers.

```console
$ curl -X POST ... http://0.0.0.0:5000/v0/node/base?user=dockerfile
```

We can also provide the docker server we want our image to be deploy to.

```console
$ curl -X POST ... http://0.0.0.0:5000/v0/node/base?where=tcp://172.17.0.6:4243
```


### Destruction

```console
curl -X DELETE http://0.0.0.0:5000/v0/node/base -H "Authorization:$TEST_API_KEY"
{
    "destroyed": true,
    "name": "hivetech-base",
    "unregistration": {
        "message": "not implemented",
        "success": false
    }
}
```


## Node interactions

### Image state

We can fetch some informations about a running node.

```console
$ # Again this is a protected resource
$ curl http://0.0.0.0:5000/v0/node/base
{
  "error": "Could not verify your access level for that URL. You have to login with proper credentials"
}
$ curl http://0.0.0.0:5000/v0/node/base -H "Authorization:$TEST_API_KEY"
{
    "acl": [],
    "ip": "http://api.unide.co:49155",
    "links": [],
    "name": "hivetech-base",
    "node": {
        "cpu": 0,
        "created": "2014-04-29T22:01:06.563456003Z",
        "env": [
            "CONSUL_MASTER=192.168.0.19",

        ...

        "virtual_ip": "172.17.0.4"
    },
    "state": {
        "ExitCode": 0,
        "FinishedAt": "0001-01-01T00:00:00Z",
        "Ghost": false,
        "Pid": 29048,
        "Running": true,
        "StartedAt": "2014-04-29T22:01:07.5853093Z"
    }
}
```

## Proxy

*Hivy* manipulates server's [Hipache](https://github.com/dotcloud/hipache)
instance to route http traffic.

The proxy is a protected resource, you must provide your api token to each request.

```console
$ curl -H "Authorization:122vezvzevz18ev4ev8ezv" ...
```

### Map 2 backends to intuition.io

```console
$ # Add as much nodes as necessary
$ # append `reset=true` to replace an existing config related to the frontend
$ curl -X POST "http://0.0.0.0:5000/v0/proxy/intuition.io?node=http://192.168.0.11&node=http://172.17.0.3:5000&name=intuition"
{'intuition.io':[
    'http://192.168.0.11',
    'http://172.17.0.3:5000'
]}
```

### Update this frontend with a new backend

```console
$ curl -X PUT "http://0.0.0.0:5000/v0/proxy/intuition.io?node=http://172.17.0.6:5000"
{'intuition.io':[
    'http://192.168.0.11',
    'http://172.17.0.3:5000',
    'http://172.17.0.6:5000'
]}
```

### Fetch the current proxy configuration

```console
$ # Replace the domain name with all to catch the whole mapping
$ curl "http://0.0.0.0:5000/v0/proxy/intuition.io"
[
    'http://192.168.0.11',
    'http://172.17.0.3:5000',
    'http://172.17.0.6:5000'
]
```

### Remove frontends

```console
$ # Replace the domain name with all to reset the proxy
$ curl -X DELETE "http://0.0.0.0:5000/v0/proxy/intuition.io"
{
    'removed': true
}
```


---
##### last modified on: May 2, 2014
---
