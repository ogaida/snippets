---
title: grep - use dash in a search string within grep
categories:
  - linux
  - bash
author: Oliver Gaida
version: 1
---

# {{ page.title }}

if i grep a multiline output for a string that contais `-linux` then i try use the following

```bash
$ printf '1-linux\n2-linux\n'
1-linux
2-linux
$ printf '1-linux\n2-linux\n'|grep -linux
# => error
```

this is because grep tries to interpret `-linux` as an option specific to grep. To shut off this behaviour just use `--` or `-e` in front of you search-string:

```bash
$ printf '1-linux\n2-linux\n'|grep -- -linux
1-linux
2-linux
$ printf '1-linux\n2-linux\n'|grep -e -linux
1-linux
2-linux
```