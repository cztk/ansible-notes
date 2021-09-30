## Introduction

We use ansible for software provisioning, configuration management and software deployment.
Later on we use a `playbook` to define the server `roles`.
A playbook can import other playbooks. Ideally we have one playbook for one server type which includes the needed roles.

`inventory` is our list of hosts per role

`playbook` describes what to do

`role` can be a service for example: grafana or mariadb

`Targets` in this documentation are `Ubuntu 20.04` if not mentioned otherwise.

**Installation**

The ansible tools are required to be installed on the host to deploy from, only.

For deb-based systems you can use
```
sudo apt install ansible
```

__Or__ on Ubuntu you can also use packages built by Ansible team using their ppa ``ppa:ansible/ansible`` if you prefer that. 
```
sudo apt install software-properties-common
sudo add-apt-repository ppa:ansible/ansible
sudo apt-get update
```

