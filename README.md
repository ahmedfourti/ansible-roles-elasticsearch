Role Name: ElasticSearch
========================

This role will install ElasticSearch.  
You can install it as stand alone or as a cluster

Requirements
------------

Java must be installed on every host  
Get the role here : https://github.com/ahmedfourti/ansible-roles-java  

Role Variables
--------------

**package_state**: The package state (present, installed, latest, absent or removed)     
**es_major_version**: The major ElasticSearch version to add repo (ie: 5.x, 6.x)   
**es_version**: The ElasticSearch version to be installed (ie: 6.1, 5.1.1..)     
**es_port**: The port to listen on, if not set, the default is 9200        
**es_transport_port**: The port used for cluster communication, if not set, the default is 9300  
**cluster**: Boolean. If true then make sure to set the right group name in the template at section "discovery.zen.ping.unicast.hosts"     
**node_name**: The name of the node. If not set, the default will be the hostname    
**cluster_name**: If you want to have a cluster, this must be set      
**path_data**: The path for logs. Defaults to /var/lib/elasticsearch    
**path_logs**: The path for logs. Defaults to /var/log/elasticsearch             
**bootstrap_memory_lock**: Lock the memory at startup. Default to "false"  
**minimum_master_nodes**: The number of minimum nodes to start cluster, this prevents "split brain". Set it only if you install cluster  
**xms**: Minimum amout of Ram to start ElasticSearch (ie: 1g, 2g, 512M)    
**xmx**: Maximum amout of Ram to start ElasticSearch (ie: 1g, 2g, 512M)       

Installation
------------

You can get this role by using ```git clone``` command.  
You can also add this repo to your ```requirements.yml``` and use ```ansible-galaxy install -r requirements.yml -p {{path_to_roles}}```  
Or you can download and unzip it in your roles directory  


Example Playbook
----------------

In this example, I have set a group [es-servers] in my inventory file.  

    ---
    - name: Deploying Demo
      hosts:
        - es-servers
      roles:
        - java
        - elasticsearch
      vars:
      
       #Role ElasticSearch
        package_state: present
        es_version: 6.1.0
        es_major_version: 6.x
        es_port: 9200
        es_transport_port: 9300
        node_name: test
        cluster_name: demo-home
        path_data: /var/lib/elasticsearch
        path_logs: /var/log/elasticsearch
        bootstrap_memory_lock: "false"
        minimum_master_nodes: 2
        xms: 512M
        xmx: 512M
        
       #Role Java
        java_packages_redhat:
          - java-1.8.0-openjdk
        java_packages_debian:
          - oracle-java8-installer

License
-------

BSD

