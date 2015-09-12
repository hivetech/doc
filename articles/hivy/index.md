---
sidebar_current: "hivy"
---

# Hivy

[![Latest Version](https://pypip.in/v/hivy/badge.png)](https://pypi.python.org/pypi/hivy/)
[![Build Status](https://drone.io/github.com/hivetech/hivy/status.png)](https://drone.io/github.com/hivetech/hivy/latest)
[![Coverage Status](https://coveralls.io/repos/hivetech/hivy/badge.png)](https://coveralls.io/r/hivetech/hivy)
[![Code Health](https://landscape.io/github/hivetech/hivy/master/landscape.png)](https://landscape.io/github/hivetech/hivy/master)
[![Requirements Status](https://requires.io/github/hivetech/hivy/requirements.png?branch=master)](https://requires.io/github/hivetech/hivy/requirements/?branch=master)
[![License](https://pypip.in/license/hivy/badge.png)](https://pypi.python.org/pypi/hivy/)
[![Gitter chat](https://badges.gitter.im/hivetech.png)](https://gitter.im/hivetech)

> Unide Hive controller

Hivy exposes a RESTful API to the [unide](unide.co) platform. Create, destroy
and configure collaborative development environments and services around it.


## Features

* High level, RESTFul interface to [docker][2]-based infrastructure
* Optimized, ssh-ready node images powered by [passenger-docker][6]
* Allow complex, real-world app scenarios with robust service discovery
* Monitoring, health checker thanks to [Consul][3]
* Flexible, distributed
* Token strategy authentification
* Server and system status
* Full control over created images through [Salt][4] and [Ansible][5]


## Installation

Docker must be [installed](http://www.docker.io/gettingstarted/) on the server
your are deploying the environments.

You also need [consul v0.1.0][3] for service orchestration.

```console
# Check your installation
$ docker version && consul version

$ (sudo) pip install hivy

$ # Default settings use local docker server (using default unix sockets)
$ # But you can tell hivy to use another one
$ export DOCKER_URL="http://172.0.1.17:4243"
```

TODO: setup salt
TODO: docker with public binding

## Usage

In a first terminal, fire up the server.

```console
$ # Note you can use a Procfile or different windows
$ consul agent -server -bootstrap -data-dir /tmp/consul -node=master
$ salt-master -l debug -c /etc/salt &
$ hivy --bind 0.0.0.0 --debug
```

And play with it in another terminal

```console
$ # Get some informations
$ curl http://0.0.0.0:5000/
{ ... versions and status ... }
curl http://0.0.0.0:5000/v0/doc
```

Learn more about [the API here](/articles/hivy/api.html).


[1]: http://unide.co
[2]: http://docker.io
[3]: http://consul.io
[4]: www.saltstack.com
[5]: www.ansible.com
[6]: https://github.com/phusion/passenger-docker

---
##### last modified on: April 29, 2014
---
