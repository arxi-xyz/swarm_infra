initial swarm manager
=========

Config docker swarm manager nodes

Requirements
------------

python3-docker package must be installed 

Role Variables
--------------

I try to specefiy the swarm leader by by boolean. consider to put the leader node as first host in inventory

``` yml
all:
  children:
    swarm:
      children:
        manager:
          hosts:
            manager_1:
              ansible_host: 192.168.56.2
              ansible_user: vm
              ansible_become_pass: password
              swarm_leader_node: true
              swarm_remote_addr: 192.168.56.2
            manager_2:
              ansible_host: 192.168.56.3
              ansible_user: vm
              ansible_become_pass: password
              swarm_remote_addr: 192.168.56.3
            manager_3:
              ansible_host: 192.168.56.4
              ansible_user: vm
              ansible_become_pass: password
              swarm_remote_addr: 192.168.56.4
```

Example Playbook
----------------

``` yml
---
- name: Install Docker and initial swarm managers
  become: true
  hosts: manager
  roles:
    - install_docker
    - initial_swarm_manager

```
License
-------

Apache2

Author
------------------
[Arxi](https://github.com/arxi-xyz)
