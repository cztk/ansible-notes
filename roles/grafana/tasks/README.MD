*grafana/tasks/main.yml*

- `install gpg`

ensures we have the needed tools installed to add the grafana pgp key in the `install gpg` rule.
It install the packages `gnupg` and `software-properties-common` as the `state` flag is set to `present`
and __not__ `absent`.
If the software list cache is older than `cache_valid_time` seconds it will run `apt update` before doing so.
As of Ansible 2.4, if explicitly set, this sets update_cache=yes.

- `add gpg key`

installs the gpg.key which is used to validate the repository. `validate_certs` is set to `yes` by `default`
however it gives me a good feeling explicitly setting it to yes, just in case behaviour changes or bugs.

- `add repository`

This adds the actual (OSS) repository line to our apt sources. `state` and `validate_certs` see above.

- `install grafana`

Instructs the system to update its available software list by setting `update_cache` to yes and install the
latest version of the grafana package.

- `start service grafana-server`

`daemon_reload` ensures systemd has read unit changes. `enabled` ensures the service _grafana-server_ is started
on boot and lastly `state` tells ansible to run the needed action to start the server now.

- `wait for service up`

here we wait until grafana webserver is accessible and returns 200 OK.
`register` is used to save the result of the executed task (`uri`) in the variable called `__result`.
As this might take a while, we loop this task `until` the condition `__result.status == 200` is matched
_or_ we reached `retries` loops, also we pause `delay` seconds for each loop iteration.

- `load admin password from vault`

we use a `vault` to save the encrypted admin password as a minimal security measurement. `include_vars` is an
instruction to load variables from the specified `file`, which is looked at in the `vars` directory, if no path is
given.


- `change admin password for grafana gui`

It is wise not to leave the default password, so we use the grafana cli tool to reset the admin password
to the one we defined using `grafana_admin_password` variable. The result of the cli execution is saved
in `__command_admin` variable and ansible shall report the task if the result code is not 0, which means
it failed.