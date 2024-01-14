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

- `-type f` only find files
- `-printf "%s\t%p\n"` print
  - `%s` size
  - `%p` filename
- `sort -nr` sort numeric and reverse