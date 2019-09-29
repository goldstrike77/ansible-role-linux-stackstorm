![](https://img.shields.io/badge/Ansible-stackstorm-green.svg?logo=angular&style=for-the-badge)

>__Please note that the original design goal of this role was more concerned with the initial installation and bootstrapping environment, which currently does not involve performing continuous maintenance, and therefore are only suitable for testing and development purposes,  should not be used in production environments.__

>__请注意，此角色的最初设计目标更关注初始安装和引导环境，目前不涉及执行连续维护，因此仅适用于测试和开发目的，不应在生产环境中使用。__
___

<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/logo_stackstorm.png" align="right" /></p>

__Table of Contents__

- [Overview](#overview)
- [Requirements](#requirements)
  * [Operating systems](#operating-systems)
  * [StackStorm Versions](#stackstorm-versions)
- [ Role variables](#Role-variables)
  * [Main Configuration](#Main-parameters)
  * [Other Configuration](#Other-parameters)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Hosts inventory file](#Hosts-inventory-file)
  * [Vars in role configuration](#vars-in-role-configuration)
  * [Combination of group vars and playbook](#combination-of-group-vars-and-playbook)
- [License](#license)
- [Author Information](#author-information)
- [Contributors](#Contributors)

## Overview
This Ansible role installs StackStorm on linux operating system, including establishing a filesystem structure and server configuration with some common operational features.

## Requirements
### Operating systems
This role will work on the following operating systems:

  * CentOS 7

### stackstorm versions

The following list of supported the StackStorm releases:

  * StackStorm 3.1+

## Role variables
### Main parameters #
There are some variables in defaults/main.yml which can (Or needs to) be overridden:

##### General parameters
* `st2_version:` Specify the StackStorm version.
* `st2_sys_user:` Define StackStorm system user.
* `st2_auth_user:` File-based authentication username.
* `st2_auth_pass:` File-based authentication password.
* `st2_cluster:` Cluster name of servers that implements distribution performance.
* `st2_path:` This directory is used to store state.

##### Listen port
* `st2_port:` StackStorm server listen.

##### Log Variables
* `st2_syslog_port:` Defines the input port of a syslog server for log.
* `st2_syslog_protocol:` Defines the input protocol of a syslog server for log.
* `st2_syslog_server:` Defines the address list of a syslog server.

##### Role dependencies
* `st2_mongod_dept:` A boolean value, whether MongoDB database use the same environment.
* `st2_pgsql_dept:` A boolean value, whether PostgreSQL database use the same environment.
* `st2_rabbitmq_dept:` A boolean value, whether RabbitMQ use the same environment.
* `st2_ngx_dept:` A boolean value, whether proxy web interface and API traffic using NGinx.

##### MongoDB parameters
* `st2_mongod_auth:` A boolean value, Enable or Disable MongoDB authentication.
* `st2_mongod_hosts:` Group of MongoDB hosts StackStorm should connect to.
* `st2_mongod_node_role:` Member role for ReplicaSet.
* `st2_mongod_path:` Specify the MongoDB data directory.
* `st2_mongod_port:` The MongoDB instance port.
* `st2_mongod_replset:` MongoDB ReplicaSet name.
* `st2_mongod_sa_pass:` MongoDB Superuser password.
* `st2_mongod_sa_user:` MongoDB Superuser name.
* `st2_mongod_user:` MongoDB username.
* `st2_mongod_pass:` MongoDB password.
* `st2_mongod_version:` Specify the MongoDB version, only 34.

##### PostgreSQL parameters
* `st2_pgsql_host:` PostgreSQL instance communication address.
* `st2_pgsql_mailto:` PostgreSQL report mail recipient.
* `st2_pgsql_path:` Specify the PostgreSQL data directory.
* `st2_pgsql_port:` PostgreSQL instance communication ports.
* `st2_pgsql_sa_pass:` PostgreSQL root account password.
* `st2_pgsql_backupset_arg:` PostgreSQL backup parameters.
* `st2_pgsql_bu_dbs_arg:` StackStorm Database Variables.

##### RabbitMQ parameters
* `st2_rabbitmq_host:` RabbitMQ instance communication address.
* `st2_rabbitmq_path:` Specify the RabbitMQ data directory.
* `st2_rabbitmq_bu_arg:` RabbitMQ authentication variables.
* `st2_rabbitmq_port:` RabbitMQ server listen.

##### NGinx parameters
* `st2_ngx_block_agents:` Enables or disables block unsafe User Agents.
* `st2_ngx_block_string:` Enables or disables block includes Exploits / File injections / Spam / SQL injections.
* `st2_ngx_compress:` Enables or disables compression.
* `st2_ngx_domain:` Defines domain name.
* `st2_ngx_pagespeed:` Enables or disables pagespeed modules.
* `st2_ngx_port_http:` NGinx HTTP listen port.
* `st2_ngx_port_https:` NGinx HTTPs listen port.
* `st2_ngx_ssl_protocols:` intermediate or modern, defines SSL protocol profile.
* `st2_ngx_version:` extras or standard.

##### ChatOps parameters
* `st2_chatops_hubot_adapter:` StackStorm ChatOps hubot adapter.

##### Service Mesh
* `environments:` Define the service environment.
* `tags:` Define the service custom label.
* `exporter_is_install:` Whether to install prometheus exporter.
* `consul_public_register:` Whether register a exporter service with public consul client.
* `consul_public_exporter_token:` Public Consul client ACL token.
* `consul_public_http_port:` The consul HTTP API port.
* `consul_public_clients:` List of public consul clients.

### Other parameters
There are some variables in vars/main.yml:

## Dependencies
- Ansible versions >= 2.8 are supported.
- [NGinx](https://github.com/goldstrike77/ansible-role-linux-nginx.git)
- [MongoDB](https://github.com/goldstrike77/ansible-role-linux-mongodb.git)
- [RabbitMQ](https://github.com/goldstrike77/ansible-role-linux-rabbitmq.git) 
- [PostgreSQL](https://github.com/goldstrike77/ansible-role-linux-postgresql.git)  

## Example

### Hosts inventory file
See tests/inventory for an example.

    node01 ansible_host='192.168.1.10' st2_version='3.1.0'

### Vars in role configuration
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - role: ansible-role-linux-stackstorm
           st2_version: '3.1.0'

### Combination of group vars and playbook
You can also use the group_vars or the host_vars files for setting the variables needed for this role. File you should change: group_vars/all or host_vars/`group_name`

    st2_version: '3.1.0'
    st2_sys_user: 'stanley'
    st2_auth_user: 'st2admin'
    st2_auth_pass: 'changeme'
    st2_cluster: 'st2'
    st2_path: '/data'
    st2_port:
      api: '29101'
      auth: '29100'
      exporter: '9102'
      metrics: '9125'
      mistral: '28989'
      stream: '29102'
    st2_syslog_port: '1514'
    st2_syslog_protocol: 'udp'
    st2_syslog_server:
      - '127.0.0.1'
    st2_mongod_dept: true
    st2_pgsql_dept: true
    st2_rabbitmq_dept: true
    st2_ngx_dept: true
    st2_mongod_auth: true
    st2_mongod_hosts:
      - '127.0.0.1'
    st2_mongod_node_role: 'replica'
    st2_mongod_path: '{{ st2_path }}'
    st2_mongod_port: '27017'
    st2_mongod_replset: '{{ st2_cluster }}'
    st2_mongod_sa_pass: 'changeme'
    st2_mongod_sa_user: 'sa'
    st2_mongod_user: 'st2'
    st2_mongod_pass: 'changeme'
    st2_mongod_version: '34'
    st2_pgsql_host: '{{ ansible_default_ipv4.address }}'
    st2_pgsql_mailto: 'somebody@example.com'
    st2_pgsql_path: '{{ st2_path }}'
    st2_pgsql_port: '5432'
    st2_pgsql_sa_pass: 'changeme'
    st2_pgsql_backupset_arg:
      keep: '2'
      encryptkey: 'DfqaO09ybWcme77rgoImSVq1UB9PO1al' 
    st2_pgsql_bu_dbs_arg:
      - dbs: 'mistral'
        user: 'mistral'
        pass: 'changeme'
        priv: 'ALL'
        role: 'SUPERUSER'
        net: '{{ st2_pgsql_host }}/32'
    st2_rabbitmq_host: '{{ ansible_default_ipv4.address }}'
    st2_rabbitmq_path: '{{ st2_path }}'
    st2_rabbitmq_bu_arg:
      - vhost: '/'
        user: 'st2'
        pass: 'changeme'
        read_priv: '.*'
        write_priv: '.*'
        configure_priv: '.*'
        tags: 'StackStorm'
    st2_rabbitmq_port:
      epmd: '4369'
      erlang_dist_client: '35672-35682'
      erlang_dist_server: '25672'
      exporter: '9419'
      http: '15672'
      ssl: '5671'
      tcp: '5672'
    st2_ngx_block_agents: true
    st2_ngx_block_string: true
    st2_ngx_compress: true
    st2_ngx_domain: 'st2.example.com'
    st2_ngx_pagespeed: true
    st2_ngx_port_http: '80'
    st2_ngx_port_https: '443'
    st2_ngx_ssl_protocols: 'modern'
    st2_ngx_version: 'extras'
    st2_chatops_hubot_adapter: 'shell'
    environments: 'SIT'
    tags:
      subscription: 'default'
      owner: 'nobody'
      department: 'Infrastructure'
      organization: 'The Company'
      region: 'IDC01'
    exporter_is_install: false
    consul_public_register: false
    consul_public_exporter_token: '00000000-0000-0000-0000-000000000000'
    consul_public_http_port: '8500'
    consul_public_clients:
      - '127.0.0.1'

## License
![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## Author Information
Please send your suggestions to make this role better.

## Contributors
Special thanks to the [Connext Information Technology](http://www.connext.com.cn) for their contributions to this role.
