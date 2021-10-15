Ansible Role: Firewalld
=========
This ansible role installs firewalld and allows for easy firewall 
configuration via variables. 

When managing a lot of ports this role becomes particularly useful due 
to its capability to specify lists of ports and services per zone.


Requirements
------------
For configuration the ansible module [firewalld](https://docs.ansible.com/ansible/latest/collections/ansible/posix/firewalld_module.html) is used.

Variables
------------
List of firewalls to disable via Ansible's service module:
```
firewalld_disable_firewalls: []
```

A list of port definitions:
```
firewalld_ports: []
```

A list of service definitions:
```
firewalld_services: []
```

Example Playbook
------------
```
- hosts: all
  vars_files:
    - vars/main.yml
  roles:
    - probosmo.firewalld
```

With `vars/main.yaml`:
```
firewalld_disable_firewalls:
  - ufw

firewalld_ports:
  - zone: public
    port_numbers:
      - 80
      - 443
      - 8080-8089
    protocol: tcp
    state: enabled

firewalld_services:
  - zone: public
    service_names:
      - ssh
    state: disabled

```


License
------------
MIT
