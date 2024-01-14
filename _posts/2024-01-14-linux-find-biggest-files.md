---
title: find - the ten biggest files in the current directory
categories:
  - linux
  - bash
author: Oliver Gaida
version: 1
---

# {{ page.title }}

find the 10 biggest files in the current directory

```bash
find . -type f -printf "%s\t%p\n" | sort -nr | head -10
```
