---
title:  "sort by ipaddress"
category: bash
author: Oliver Gaida
version: 1
---

# das hosts File nach Ipadressen sortieren

```bash
cat /etc/hosts  | sort -t . -k 1,1n  -k 2,2n -k 3,3n -k 4,4n
```
