Docker installer
=========

Just installing docker :)



Role Variables
--------------
The only Variable exists in this role is docker apt packages. these variables is used for 2 task one for clean up and second for installation

```yaml
# vars/main.yml
docker_packages:
  - docker-ce
  - docker-ce-cli
  - containerd.io
  - docker-buildx-plugin
  - docker-compose-plugin  
```


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

- name: Install Docker on vm
  become: true
  hosts: swarm
  roles:
    - install_docker

License
-------

Apache2

Author
------------------
[Arxi](https://github.com/arxi-xyz)
