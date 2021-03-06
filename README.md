Role Name
=========

The Logstash portion of the Elastic Stack, aka ELK.  Known to work with Amazon's Elasticsearch Service.

Requirements
------------

TODO

Role Variables
--------------

* elastic_logstash_install: true
* elastic_logstash_syslog_port: 5514
* elastic_logstash_syslog_time_zone: UTC
* elastic_logstash_gelf_port: 12201
* elastic_elasticsearch_host: change.me.example.com
* elastic_elasticsearch_port: 9120
* elastic_stack_version: 5.x

Dependencies
------------

* kurron.base

Example Playbook
----------------

```
- hosts: servers
  roles:
      - { role: kurron.logstash, elastic_elasticsearch_host: search.example.com }
```

Logstash is configured to accept `syslog` messages at a custom port of `5514`.
Logstash is also configured to accept `GELF` formatted messages on port `12201`.

To test your installation, you can issue the following two commands, replacing the ip
with your host's ip.  The messages should show up in Kibana.  You will have to add
the proper indices into Kibana before the messages show up.

```
logger --server 192.168.1.78 --port 5514 --priority 0  --tag test 'Hello, Syslog!'

echo '{"version": "1.1","host":"example.org","short_message":"Hello, GELF!","full_message":"More details","level":1,"_user_id":9001,"_some_info":"foo","_some_env_var":"bar"}' | gzip | nc --udp --wait 1 192.168.1.78 12201
```

The configurations for the different inputs are located in `/etc/logstash/conf.d`.  Add/modify as needed.

License
-------

This project is licensed under the [Apache License Version 2.0, January 2004](http://www.apache.org/licenses/).

Author Information
------------------

[Author's website](http://jvmguy.com/).
