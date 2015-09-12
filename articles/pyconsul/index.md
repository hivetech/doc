---
sidebar_current: "pyconsul"
---

# PyConsul

[![Latest Version](https://pypip.in/v/pyconsul/badge.png)](https://pypi.python.org/pypi/pyconsul/)
[![Build Status](https://drone.io/github.com/hackliff/pyconsul/status.png)](https://drone.io/github.com/hackliff/pyconsul/latest)
[![Coverage Status](https://coveralls.io/repos/hackliff/pyconsul/badge.png)](https://coveralls.io/r/hackliff/pyconsul)
[![Requirements Status](https://requires.io/github/hackliff/pyconsul/requirements.png?branch=master)](https://requires.io/github/hackliff/pyconsul/requirements/?branch=master)
[![License](https://pypip.in/license/pyconsul/badge.png)](https://pypi.python.org/pypi/pyconsul/)

> Python client for [Consul][1]


A dummy, one-file implementation on top of the [HTTP API][5] of Consul.

## Install

* Install Consul following [the official guide][3], or this one-liner:

```console
$ # Install consul 0.1.0_linux_amd64 under /usr/local/bin
$ wget -qO- https://raw.githubusercontent.com/hackliff/pyconsul/master/install-consul.sh | (sudo) bash
```

* Install pyconsul library

```console
$ (sudo) pip install pyconsul
```


## Getting started

You should probably become familiar with [the official Consul documentation][4]
before playing around with pyconsul, and [the HTTP API][5] especially.

First, we need an agent in server mode.

```console
consul agent -server -bootstrap \
  -data-dir /tmp/consul \
  -node=agent-one \
  -client=192.168.0.19 \
  -bind=0.0.0.0
```

Optionally, on different hosts, we launch more consul agents in client mode.

```console
$ # Replace with the address provided above to `--client`
$ consul agent --join 192.168.0.19 -data-dir /tmp/consul
```

Then we can interact with them.


### High level usage

```python
from pyconsul.http import Consul

# `host` meets `-client <host>` arg of consul (default to 127.0.0.1)
consul_ = Consul(host='0.0.0.0', port=8500)

consul_.status
# {'leader': u'192.168.0.19:8300', 'peers': [u'192.168.0.19:8300']}
# Or invidually
consul_.status, consul_.peers

# Get cluster topology
consul_.datacenters
# [u'dc1']
consul_.nodes
# [
#   {u'Address': u'192.168.0.19', u'Node': u'agent-one'},
#   {u'Address': u'172.17.0.3', u'Node': u'sandbox'}
# ]
consul_.services
{u'consul': None}

# Or inspect specific nodes and services
consul_.node('agent-one')
# {
#   u'Node': {u'Address': u'192.168.0.19', u'Node': u'agent-one'},
#   u'Services': {
#       u'consul': {
#           u'ID': u'consul',
#           u'Port': 8300,
#           u'Service': u'consul',
#           u'Tags': None
#       }
#   }
# }
consul_.service('web')
# []
```


### Cluster health

```python
# We can monitor various cluster states

consul_.health(node='agent-one')
# [{u'CheckID': u'serfHealth',
#   u'Name': u'Serf Health Status',
#   u'Node': u'master',
#   u'Notes': u'',
#   u'ServiceID': u'',
#   u'ServiceName': u'',
#   u'Status': u'passing'}
# ]
# Or we can target more generally services
# Return the ones marked as 'critical'
consul_.health(state='critical')
# []
consul_.health(checks='web')
# []
consul_.health(service='web')
# []
```


### Storage

```python
# Access key / value storage
# `cas` and `flag` parameters are supported
consul_.storage.set('node/name', 'test')
# True

# Under the hood, values are base64 encoded to support UTF-8
# but pyconsul decodes it before returning
consul_.storage.get('node/name')
# [{
#   u'CreateIndex': 42,
#   u'Flags': 0,
#   u'Key': u'node/name',
#   u'ModifyIndex': 42,
#   u'Value': 'test'
# }]
consul_.storage.delete('node/name')
# {'success': True}
```

We can also use the storage API as a standalone object

```python
from pyconsul.http import KVStorage

# KVStorage shares the same abstract constructor as Consul
storage = KVStorage()
# Set the key only if it doesn't already exist
storage.set('project', 'pyconsul', cas=0)
# [{
#   u'CreateIndex': 49,
#   u'Flags': 0,
#   u'Key': u'state',
#   u'ModifyIndex': 49,
#   u'Value': 'pyconsul'
# }]
storage.set('project/doc', 'in progress', cas=0)
# ...

# Let's retrieve everything under the key `project`
storage.get('project', recurse=True)
# [{
#     u'CreateIndex': 54,
#     u'Flags': 0,
#     u'Key': u'state/project',
#     u'ModifyIndex': 54,
#     u'Value': 'in construction'
#  },
#  {
#     u'CreateIndex': 49,
#     u'Flags': 0,
#     u'Key': u'state',
#     u'ModifyIndex': 49,
#     u'Value': 'ok'
# }]

storage.delete('project', recurse=True)
# {'success': True}
storage.get('project', recurse=True)
# {'error': 'Not Found', 'status': 404}
```


### Local agent

Get back to our `consul_`, we can manage the agent running locally

```python
# Like we did with `storage`, the local agent is available as a standalone
# object, sharing the same constructor
#     agent = pyconsul.http.Agent()
# Or as an attribute of `consul_`
#     agent = consul_.local_agent

# We can access useful attributes
agent.members
# [{
#   u'Addr': u'192.168.0.19',
#   u'DelegateCur': 4,
#   u'DelegateMax': 4,
#   u'DelegateMin': 2,
#   u'Name': u'agent-one',
#   u'Port': 8301,
#   u'ProtocolCur': 2,
#   u'ProtocolMax': 2,
#   u'ProtocolMin': 1,
#   u'Status': 1,
#   u'Tags': {
#     u'bootstrap': u'1',
#     u'dc': u'dc1',
#     u'port': u'8300',
#     u'role': u'consul',
#     u'vsn': u'1',
#     u'vsn_max': u'1',
#     u'vsn_min': u'1'
#   }
# }]
agent.services
# {}
agent.checks
# {}
```

We can also trigger actions.

```python
agent.join('172.17.0.3')
# {'success': True}
# Force 'agent-two' into 'left state'
agent.force_leave('agent-two')
# {'success': True}
```


## License

Copyright 2014 Xavier Bruhiere.

PyConsul is available under the [MIT Licence][2].


[1]: http://consul.io
[2]: http://opensource.org/licenses/MIT
[3]: http://www.consul.io/intro/getting-started/install.html
[4]: http://www.consul.io/intro/
[5]: http://www.consul.io/docs/agent/http.html

---
##### last modified on: April 29, 2014
---
