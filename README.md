MongoDB
=========

An Ansible Role that installs and configures MongoDB

Requirements
------------
### Ansible User Prerequisites

Some tasks of this role need to be run as root(thanks to condition 'when ansible_user_id == root')
So, a 'non-root' user just can deploy configuration files under conf.d directory.
Nginx installation and settings are reserved by root user.

### Operating Systems support

* Centos 7
* Redhat 7,8


Dependencies
------------

You(with good rights) can use 'users' role as a dependency, when it is required to create user accounts used by application (like 'mongod' user)

Variables and Properties
------------------------

In OPS ui, when you design your application, you have to use the software model(provider: ansible) related to this role
and so you benefited from data form

## Role Variables

| Variables | Required | Default value | Description |
|-----------|----------|---------------|-------------|
| mongodb_version | False | *'4.4'* | Major version of elasticsearch package from elasticsearch repository |
| mongodb_disable_install | False | *false* | Will skip packages installation, service managed and directories creation. |
| mongodb_package | False | *mongodb-org* | package name which must be installed |
| mongodb_create_config | False | *true* | Will create custom mongod.conf config file and all other files and directories. |
| mongodb_enabled_on_boot | False | *true* | enabled systemd service on boot(as root user) |
| mongodb_disable_http_proxies | False | *false* | disable proxy usage in mongodb installation process. |
| mongodb_https_proxy | False | *http://proxy-prod-scl.svc.meshcore.net:3128* | https proxy address |
| mongodb_http_proxy | False | *http://proxy-prod-scl.svc.meshcore.net:3128* | http proxy address |
| mongodb_systemlog_verbosity | False | *0* | The verbosity level determines the amount of Informational and Debug messages MongoDB outputs |
| mongodb_systemlog_traceAllExceptions | False | *false* | Print verbose information for debugging. Use for additional logging for support-related troubleshooting. |
| mongodb_systemlog_destination | False | *'file'* | systemlog destination (https://docs.mongodb.com/manual/reference/configuration-options/) |
| mongodb_systemlog_syslogFacility | False | *'user'* | The facility level used when logging messages to syslog. |
| mongodb_systemlog_path | False | *'/var/log/mongodb/mongod.log'* | The path of the log file to which mongod or mongos should send all diagnostic logging information. |
| mongodb_systemlog_logappend | False | *false* | When true, mongos or mongod appends new entries to the end of the existing log file when the mongos or mongod instance restarts. Without this option, mongod will back up the existing log and create a new file. |
| mongodb_systemlog_logrotate | False | *'rename'* | The behavior for the logRotate command. |
| mongodb_systemlog_timeStampFormat | False | *'iso8601-local'* | The time format for timestamps in log messages. |
| mongodb_storage_dbpath | False | *'/var/lib/mongo'* | The directory where the mongod instance stores its data. |
| mongodb_storage_dirperdb | False | *false* | When true, MongoDB uses a separate directory to store data for each database. |
| mongodb_storage_engine | False | *'wiredTiger'* | The storage engine for the mongod database. |
| mongodb_storage_journal_enabled | False | *true* | Enable or disable the durability journal to ensure data files remain valid and recoverable. |
| mongodb_storage_inMemorySizeGB | False | *''* | Maximum amount of memory to allocate for in-memory storage engine data, including indexes, oplog if the mongod is part of replica set, replica set or sharded cluster metadata, etc. |
| mongodb_wiredtiger_cache_sizegb | False | *''* | Defines the maximum size of the internal cache that WiredTiger will use for all data. |
| mongodb_wiredtiger_directory_for_indexes | False | *false* | When true mongod stores indexes and collections in separate subdirectories under the data directory. |
| mongodb_net_port | False | *27017* | The TCP port on which the MongoDB instance listens for client connections. |
| mongodb_net_bindip | False | *0.0.0.0* | The hostnames and/or IP addresses and/or full Unix domain socket paths on which mongos or mongod should listen for client connections. |
| mongodb_net_ipv6 | False | *false* | Set to true to enable IPv6 support. |
| mongodb_net_maxconns | False | *65536* | The maximum number of simultaneous connections that mongos or mongod will accept. |
| mongodb_net_ssl | False | *false* | enable usage SSL |
| mongodb_net_ssl_keyfile | False | *""* | The .pem file that contains both the TLS certificate and key. |
| mongodb_net_ssl_cafile | False | *""* | The .pem file that contains the root certificate chain from the Certificate Authority. |
| mongodb_net_ssl_clusterfile | False | *""* | The .pem file that contains the x.509 certificate-key file for membership authentication for the cluster or replica set. |
| mongodb_net_ssl_location | False | */etc/mongodb/ssl* | directory where stores certificate files |
| mongodb_security_authorization | False | *"disabled"* | Enable or disable Role-Based Access Control (RBAC) to govern each user's access to database resources and operations. |
| mongodb_security_keyfile | False | *""* | key file that stores the shared secret that MongoDB instances use to authenticate to each other in a sharded cluster or replica set. |
| mongodb_security_javascript_enabled | False | *true* | Enables or disables server-side JavaScript execution. |
| mongodb_operation_profiling_slow_op_threshold_ms | False | *100* | The slow operation time threshold, in milliseconds. Operations that run for longer than this threshold are considered slow. |
| mongodb_operation_profiling_mode | False | *"off"* | Specifies which operations should be profiled. |
| mongodb_enable_replication | False | *false* | enable replication |
| mongodb_replication_replSetName | False | *""* | The name of the replica set that the mongod is part of. All hosts in the replica set must have the same set name. |
| mongodb_replication_oplogsize | False | *1024* | The maximum size in megabytes for the replication operation log. |
| mongodb_set_parameters | False | *""* | Set MongoDB parameter or parameters described in MongoDB Server Parameters <parameter1>: <value1> |
### Role Vars file

By example, I would like to install(as root user) elasticsearch and set configuration files, place following content into vars yaml file

```yaml
---
mongodb_version: '4.4'
mongodb_disable_install: false
mongodb_package: mongodb-org
mongodb_create_config: true
mongodb_enabled_on_boot: true

mongodb_disable_http_proxies: false
mongodb_https_proxy: http://proxy-prod-scl.svc.meshcore.net:3128
mongodb_http_proxy: http://proxy-prod-scl.svc.meshcore.net:3128

mongodb_systemlog_verbosity: 0
mongodb_systemlog_traceAllExceptions: false
mongodb_systemlog_destination: 'file'
mongodb_systemlog_syslogFacility: 'user'
mongodb_systemlog_path: '/var/log/mongodb/mongod.log'
mongodb_systemlog_logappend: false
mongodb_systemlog_logrotate: 'rename'
mongodb_systemlog_timeStampFormat: 'iso8601-local'

mongodb_storage_dbpath: '/var/lib/mongo'
mongodb_storage_dirperdb: false
mongodb_storage_engine: 'wiredTiger'
mongodb_storage_journal_enabled: true
mongodb_storage_inMemorySizeGB: ''
mongodb_wiredtiger_cache_sizegb: ''
mongodb_wiredtiger_directory_for_indexes: false

mongodb_net_port: 27017
mongodb_net_bindip: 0.0.0.0
mongodb_net_ipv6: false
mongodb_net_maxconns: 65536
mongodb_net_ssl: false
mongodb_net_ssl_keyfile: ""
mongodb_net_ssl_cafile: ""
mongodb_net_ssl_clusterfile: ""
mongodb_net_ssl_location: /etc/mongodb/ssl

mongodb_security_authorization: "disabled"
mongodb_security_keyfile: ""
mongodb_security_javascript_enabled: true

mongodb_operation_profiling_slow_op_threshold_ms: 100
mongodb_operation_profiling_mode: "off"

mongodb_enable_replication: false
mongodb_replication_replSetName: ""
mongodb_replication_oplogsize: 1024

mongodb_set_parameters:

```

Example Playbook
----------------

Including an example of how to use your role :
```yaml
---
    - hosts: servers
      vars_files:
        - vars_file.yml
      roles:
        - role: mongodb
```

The tests were done by using molecule integration test(inspec)
[More info](molecule-README.md#Requirements)

License
-------

BSD

Author Information
------------------
samvelisoyan@hotmail.com
