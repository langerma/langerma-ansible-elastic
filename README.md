# langerma-ansible-elasticsearch

an ansible role to install and configure elasticsearch on rhel/centos 7

## sample playbook
```yml
- hosts: all
  remote_user: someuser
  become: true
  vars:
    java_install_dir: /app/java
    java_version: 11
    elasticsearch_version: 6.5.4
    elasticsearch_install_dir: /app/elasticsearch
    elasticsearch_install_tar: https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.5.4.tar.gz
    elasticsearch_instance_name: "instance-1"
    elasticsearch_data_dirs:
      - "/app/data/elasticsearch"
    elasticsearch_config:
    #node.name: "node1"
      cluster.name: "custom-cluster"
      discovery.zen.ping.unicast.hosts: "master"
      network.host: [_site_,_local_]
      http.port: 9200
      transport.tcp.port: 9300
      node.data: true
      node.master: true
      bootstrap.memory_lock: true
    elasticsearch_scripts: false
    elasticsearch_templates: false
    elasticsearch_version_lock: false
    elasticsearch_heap_size: 256m
    elasticsearch_api_port: 9200
  roles:
      - role: langerma-ansible-elastic
```
