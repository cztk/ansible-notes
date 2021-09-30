## ansible.cfg

certain configurations are the same for each host in a mass deployment.
We specify the default inventory file and ssh user and private key file which will be used
for each host.

```
[defaults]
inventory = inventory.yml
remote_user = <YOUR USER>
private_key_file =  <PATH TO KEY_FILE>
```