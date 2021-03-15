---
title: "Ansible ipaddr Filter"
category: ansible
author: Oliver Gaida
version: 1
---

eventuell vorher das notwendige Python-Modul installieren

```bash
python -m pip install netaddr
```

# Ansible ipaddr Beispiele

## lokale Facts dumpen:

```bash
ansible localhost -m setup --tree ./
```

## mit jq infos saugen

```bash
jq -r '.ansible_facts.ansible_default_ipv4|.network+"/"+.netmask' localhost
192.168.4.0/255.255.255.0
```

Nun das ganze durch den Filter jagen und zu CIDR konvertieren

<!--{% raw %} -->

```bash
ansible localhost -m debug -a "msg={{ net_mask | ansible.netcommon.ipaddr('net') }}" -e net_mask=$(jq -r '.ansible_facts.ansible_default_ipv4|.network+"/"+.netmask' localhost)
localhost | SUCCESS => {
    "msg": "192.168.4.0/24"
}
```

<!--{% endraw %} -->

siehe [https://docs.ansible.com/ansible/latest/user_guide/playbooks_filters_ipaddr.html#converting-subnet-masks-to-cidr-notation](https://docs.ansible.com/ansible/latest/user_guide/playbooks_filters_ipaddr.html#converting-subnet-masks-to-cidr-notation)