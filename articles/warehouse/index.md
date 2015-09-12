---
sidebar_current: "warehouse"
---

# Warehouse

> Hive images

## Base node

* Powerful docker image based on ubuntu 12.04 LTS: [phusion/passenger-customizable:0.9.9](https://github.com/phusion/passenger-docker)
* ssh ready, key-based authentification
* runnit process manager
* python installed

```console
$ docker run -d --name myapp \
    -e SALT_MASTER=192.168.0.11 \
    -e CONSUL_MASTER=192.168.0.11 \
    -e LOGSTASH_SERVER=172.17.0.3 \
    -e NODE_ID=myapp \
    hivetech/base /sbin/my_init --enable-insecure-key
```

Some remarks

* NODE_ID has a default value of $(hostname)
* Without specifying SALT_MASTER, no minion will run
* Without specifying CONSUL_MASTER, no consul agent will run
* Without specifying LOGSTASH_SERVER, no logstash-forwarder agent will run, neither collectd daemon

### Perf monitoring with [collecd][1]

### Logs management with [Logstash-forwarder][2]

### Service discovery and monitoring with [consul][3]

### Configuration management with [Salt][4] and [Ansible][5]


## Central metrics management and vizualisation


Stack

* [Logstash][6]
* [Elasticsearch][7]
* [Kibana][8]

```console
$ docker run -d --name logstash \
    -p 9200:9200 -p 9292:9292 quay.io/hackliff/logstash
```


## Domain management with [Hipache][9]


[1]: https://collectd.org
[2]: https://github.com/elasticsearch/logstash-forwarder
[3]: http://consul.io/
[4]: http://www.saltstack.com/
[5]: http://www.ansible.com/home
[6]: http://logstash.net/
[7]: http://www.elasticsearch.org/
[8]: http://www.elasticsearch.org/overview/kibana/
[9]: https://github.com/dotcloud/hipache
[10]: https://github.com/phusion/passenger-docker

---
##### last modified on: May 8, 2014
---
