---
title:  "how to get the remote ip of the current host"
category: 
  - ansible
author: Oliver Gaida
version: 2
---

# my inventory

```ini
testhost ansible_host=192.168.3.4
```

# how to get this ip when running ansible

Here the dictionary `hostvars` and the variable `inventory_hostname` help us. `hostvars` includes every variable from wherever it comes and the  
`inventory_hostname` contains the hostname of the current host itself. So with `hostvars[inventory_hostname]` I can access a dictionary with all Properties of the current host.

<!--{% raw %} -->

```bash
ansible testhost -m debug -a "msg={{ hostvars[inventory_hostname].ansible_host }}"
prox61 | SUCCESS => {
    "msg": "192.168.3.4"
}
```

<!--{% endraw %} -->

There are many other variables which are very usefull:

- ansible_user
- group_names
- ansible_ssh_common_args
- ansible_config_file
- playbook_dir