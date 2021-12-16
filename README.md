ansible-role-dhcpd
=========

Install and configure dhcp server

Requirements
------------

RHEL8 or above

Role Variables
--------------

* `dhcpd_packages` - list of packages to install
* `dhcpd_conf_file` - full path to dhcpd.conf
* `dhcpd_service_name` - systemd service name of dhcpd
* `dhcpd_service_enable` - boolean to enable dhcpd on boot
* `dhcpd_global_params` - list of global parameters, example:

```yaml
dhcpd_global_params:
  - key: authoritative
  - key: option routers
    value: 192.168.1.1
```

* `dhcpd_subnets` - list of subnets, example:

```yaml
dhcpd_subnets:
  - network: 192.168.1.0
    netmask: 255.255.255.0
    routers: 192.168.1.1
    subnet_mask: 255.255.255.0
    domain_name_servers:
      - 1.1.1.1
      - 2.2.2.2
    range_start: 192.168.1.100
    range_end: 192.168.1.120
    hosts:
      - name: myhost
        mac: 12:a2:0a:e3:5f:74
        ip: 192.168.1.2
```

Dependencies
------------

Collections:

* `ansible.builtin`

Example Playbook
----------------

```yaml
- hosts: myhosts
  vars:
    dhcpd_global_params:
      - key: authoritative
    dhcpd_subnets:
      - network: 192.168.1.0
        netmask: 255.255.255.0
        routers: 192.168.1.1
        subnet_mask: 255.255.255.0
        domain_name_servers:
          - 1.1.1.1
          - 2.2.2.2
        range_start: 192.168.1.100
        range_end: 192.168.1.120
  roles:
    - ansible-role-dhcpd
```

License
-------

GPLv3

Author Information
------------------

Vladimir Vasilev
