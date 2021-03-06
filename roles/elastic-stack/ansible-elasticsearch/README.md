Ansible Role: Elasticsearch
===========================

An Ansible Role that installs [Elasticsearch](https://www.elastic.co/products/elasticsearch).

Requirements
------------

This role will work on:
 * Red Hat
 * CentOS
 * Fedora
 * Debian
 * Ubuntu

Role Variables
--------------

Defaults variables are listed below, along with its values (see `defaults/main.yml`):

```
  elasticsearch_cluster_name: wazuh
  elasticsearch_node_name: node-1
  elasticsearch_http_port: 9200
  elasticsearch_network_host: 127.0.0.1
  elasticsearch_jvm_xms: 1g
  elastic_stack_version: 5.5.0
```

Example Playbook
----------------

- Single-node
```
  - hosts: elasticsearch
    roles:
      - { role: ansible-role-elasticsearch, elasticsearch_network_host: '192.168.33.182', single_host: true }
```

- Three nodes Elasticsearch cluster
```
---
- hosts: 172.16.0.161
  roles:
    - {role: ../roles/elastic-stack/ansible-elasticsearch, elasticsearch_network_host: '172.16.0.161', elasticsearch_bootstrap_node: true, elasticsearch_cluster_nodes: ['172.16.0.162','172.16.0.163','172.16.0.161']}

- hosts: 172.16.0.162
  roles:
    - {role: ../roles/elastic-stack/ansible-elasticsearch, elasticsearch_network_host: '172.16.0.162', elasticsearch_master_candidate: true, elasticsearch_cluster_nodes: ['172.16.0.162','172.16.0.163','172.16.0.161']}

- hosts: 172.16.0.163
  roles:
    - {role: ../roles/elastic-stack/ansible-elasticsearch, elasticsearch_network_host: '172.16.0.163', elasticsearch_master_candidate: true, elasticsearch_cluster_nodes: ['172.16.0.162','172.16.0.163','172.16.0.161']}
```

License and copyright
---------------------

WAZUH Copyright (C) 2017 Wazuh Inc. (License GPLv3)

### Based on previous work from geerlingguy

 - https://github.com/geerlingguy/ansible-role-elasticsearch

### Modified by Wazuh

The playbooks have been modified by Wazuh, including some specific requirements, templates and configuration to improve integration with Wazuh ecosystem.
