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

Here are the keys:

<!--{% raw %} -->

```bash
ansible -m debug testhost -a 'msg={{ hostvars[inventory_hostname].keys() }}'
testhost | SUCCESS => {
    "msg": [
        "ansible_password",
        "ansible_become_pass",
        "searchDomain",
        "ansible_user",
        "ansible_ssh_common_args",
        "inventory_file",
        "inventory_dir",
        "ansible_host",
        "inventory_hostname",
        "inventory_hostname_short",
        "group_names",
        "ansible_facts",
        "playbook_dir",
        "ansible_playbook_python",
        "ansible_config_file",
        "groups",
        "omit",
        "ansible_version",
        "ansible_check_mode",
        "ansible_diff_mode",
        "ansible_forks",
        "ansible_inventory_sources",
        "ansible_verbosity"
    ]
}
ansible testhost -m debug -a var=ansible_host
# and now get the IP-Address:
testhost | SUCCESS => {
    "ansible_host": "192.168.3.4"
}
```

<!--{% endraw %} -->

other important variables are:

- ansible_user
- group_names
- ansible_ssh_common_args
- ansible_config_file
- playbook_dir
