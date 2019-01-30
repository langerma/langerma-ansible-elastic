# langerma-ansible-elasticsearch

an ansible role to install and configure elasticsearch on rhel/centos 7

## sample playbook
```yml
- hosts: master
  remote_user: vagrant
  become: true
  vars:
    elasticsearch_install_tar: /Users/langerma/Downloads/elastic/elasticsearch-6.5.4.tar.gz
    supervisord_ini_dir: /app/supervisord.d
    java_install_dir: /app/java
    java_version: 11
    elasticsearch_instance_name: "master"
    elasticsearch_data_dirs:
      - "/app/data/elasticsearch"
    elasticsearch_config:
      #node.name: "node1"
      cluster.name: "custom-cluster"
      discovery.zen.ping.unicast.hosts: "master1"
      network.host: [_eth1_,_local_]
      http.port: 9200
      transport.tcp.port: 9300
      node.data: false
      node.master: true
      bootstrap.memory_lock: true
    elasticsearch_scripts: false
    elasticsearch_templates: false
    elasticsearch_version_lock: false
    elasticsearch_heap_size: 128m
    elasticsearch_api_port: 9200
  roles:
    - role: langerma-ansible-elastic

- hosts: data
  remote_user: vagrant
  become: true
  vars:
    elasticsearch_install_tar: /Users/langerma/Downloads/elastic/elasticsearch-6.5.4.tar.gz
    supervisord_ini_dir: /app/supervisord.d
    java_install_dir: /app/java
    java_version: 11
    elasticsearch_instance_name: "instance-1"
    elasticsearch_data_dirs:
      - "/app/data/elasticsearch/instance-1"
    elasticsearch_config:
      #node.name: "node1"
      cluster.name: "custom-cluster"
      discovery.zen.ping.unicast.hosts: "master1"
      network.host: [_eth1_,_local_]
      http.port: 9200
      transport.tcp.port: 9300
      node.data: true
      node.master: false
      bootstrap.memory_lock: true
    elasticsearch_scripts: false
    elasticsearch_templates: false
    elasticsearch_version_lock: false
    elasticsearch_heap_size: 128m
    elasticsearch_api_port: 9200
  roles:
    - role: langerma-ansible-elastic

- hosts: data
  remote_user: vagrant
  become: true
  vars:
    elasticsearch_install_tar: /Users/langerma/Downloads/elastic/elasticsearch-6.5.4.tar.gz
    supervisord_ini_dir: /app/supervisord.d
    java_install_dir: /app/java
    java_version: 11
    elasticsearch_instance_name: "instance-2"
    elasticsearch_data_dirs:
      - "/app/data/elasticsearch/instance-2"
    elasticsearch_config:
      #node.name: "node1"
      cluster.name: "custom-cluster"
      discovery.zen.ping.unicast.hosts: "master1:9300"
      network.host: [_eth1_,_local_]
      http.port: 9201
      transport.tcp.port: 9301
      node.data: true
      node.master: false
      bootstrap.memory_lock: true
    elasticsearch_scripts: false
    elasticsearch_templates: false
    elasticsearch_version_lock: false
    elasticsearch_heap_size: 128m
    elasticsearch_api_port: 9201
  roles:
    - role: langerma-ansible-elastic
```
