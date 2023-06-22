---
title: flush output
categories:
  - linux
  - bash
author: Oliver Gaida
version: 1
---

# {{ page.title }}

```bash
cd /var/log
tail -f mail|unbuffer -p grep -F 'too many errors after' |tee -a too_many
```

unbuffer is part of expect package in ubuntu:

```bash
apt install expect
```