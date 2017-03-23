Role Name
=========

The Logstash portion of the Elastic Stack, aka ELK.

Requirements
------------

TODO

Role Variables
--------------

TODO

Dependencies
------------

* kurron.base

Example Playbook
----------------

```
- hosts: servers
  roles:
      - { role: kurron.logstash }
```

UPDATE!!!!

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
