---
title: list networkcards
categories:
  - linux
author: Oliver Gaida
version: 1
---

# {{ page.title }}

```bash
# ls -1 /sys/class/net/|grep e|while read nic; do echo "$nic $(cat /sys/class/net/$nic/address)"; done
ens160 00:50:ab:cd:ef:12
ens161 00:50:ab:cd:ef:13
```
