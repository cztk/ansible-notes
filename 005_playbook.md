## Playbook

The top level description of what to do on each host group.

*/playbook.yml*
```
- hosts: grafana
  become: yes
  become_user: root
  become_method: sudo
  roles:
    - grafana
```

To install the given roles on the grafana host group we need root privileges to install gpg key, packages ...
As best practice allowed ssh user is != root, this is why we make use of sudo to escalate our privileges and
become root.
