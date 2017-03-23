Role Name
=========

The Elastic Stack, aka ELK.

Requirements
------------

TODO

Role Variables
--------------

* elastic_elasticsearch_install: true
* elastic_elasticsearch_cluster_name: development
* elastic_elasticsearch_node_name: development
* elastic_kibana_install: true
* elastic_logstash_install: true
* elastic_logstash_syslog_port: 5514
* elastic_logstash_gelf_port: 12201
* elastic_packetbeat_install: false
* elastic_packetbeat_elasticsearch_host: 10.0.2.15
* elastic_metricbeat_install: false
* elastic_metricbeat_elasticsearch_host: 10.0.2.15
* elastic_filebeat_install: false
* elastic_filebeat_elasticsearch_host: 10.0.2.15
* elastic_x_pack_install: false
* elastic_stack_version: 5.x

Dependencies
------------

* kurron.base

Example Playbook
----------------

```
- hosts: servers
  roles:
      - { role: kurron.elastic-stack, elastic_logstash_syslog_port: 514 }
```

By default, the role installs Elasticsearch, Logstash and Kibana to the same host.
Logstash is configured to accept `syslog` messages at a custom port of `5514`.
Logstash is also configured to accept `GELF` formatted messages on port `12201`.

To tet your installation, you can issue the following two commands, replacing the ip
with your host's ip.  The messages should show up in Kibina.  You will have to add
the proper indices into Kibana before the messages show up.

```
logger --server 192.168.1.78 --port 5514 --priority 0  --tag test 'Hello, Syslog!'

echo '{"version": "1.1","host":"example.org","short_message":"Hello, GELF","full_message":"More details","level":1,"_user_id":9001,"_some_info":"foo","_some_env_var":"bar"}' | gzip | nc --udp --wait 1 192.168.1.78 12201
```
License
-------

This project is licensed under the [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/).

Author Information
------------------

[Author's website](http://jvmguy.com/).
