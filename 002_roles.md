**The roles**

Roles let you automatically load related vars, files, tasks, handlers, and other Ansible artifacts based on a known file
structure. After you group your content in roles, you can easily reuse them and share them with other users.

To bootstrap a role, we can use the following command within the current working dir

```
ansible-galaxy init roles/grafana
```

This creates a defined set of folders and files for a role in our /roles directory ( /roles/grafana ).

An Ansible role has a defined directory structure with eight main standard directories.
You must include at least one of these directories in each role.
You can omit any directories the role does not use.

By default, Ansible will look in each directory within a role for a main.yml file
for relevant content (also main.yaml and main)

There is more, check the docs
https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html?highlight=roles

For our scenario, we use roles within a playbook.
Having generated the grafana role, we can now refer to our `inventory` set of hosts called `grafana`
and the `role` which coincidentally also is called `grafana`.

```
---
- hosts: grafana
  roles:
    - grafana
```

This tells ansible to execute the grafana role on each host listed in the inventory grafana hosts group.