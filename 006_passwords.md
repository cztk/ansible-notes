## passwords

to save encrypted passwords, for example for the sudo functionality, use the following command
to create a config valid for all hosts. You can also replace `all` with any specified group e.g. `grafana`.
Of course only we use encryption doesn't mean we should share this file ;)
It is also possible to set up sudo without the need for a password, however this might defeat some other security
concepts.

```
ansible-vault create group_vars/all/ansible.yml
```
Instead of `create` you can use `edit` to modify the vault. 

This asks to enter a vault secret which we should remember to be able to decrypt the file later on.
After that it opens an editor in which we add the desired option to be encrypted e.g. 

```
ansible_become_password: "secret"
```

We can use the same method to configure the secret for the grafana admin user.
The `role` `grafana` expects `grafana_admin_password` to be present, so we set it for this group. 
Pay attention to the folder, we use the role's folder

```
ansible-vault create roles/grafana/vars/secret.yml
```

again, set the vaults secret and enter the following in the editor

```
grafana_admin_password: "secret"
```