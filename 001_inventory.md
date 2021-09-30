**The inventory**

We start of with our `all` group as root element. `Children` of _all_ should correspond to a `role`
like grafana, prometheus and so on.
Every `group` contains a `hosts` section declaring the host IP addresses where the role should be
executed on.

For example
/inventory.yml
```
all:
  children:
    grafana:
      hosts:
        192.0.2.2
    prometheus:
      hosts:
        192.0.2.2
    node_exporter:
      hosts:
        192.0.2.3
        192.0.2.4
        192.0.2.5
```