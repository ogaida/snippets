---
title: "powershell - search string recursive in folder "
category: powershell
author: Oliver Gaida
version: 2
---

# powershell - search string recursive in folder

```powershell
Get-ChildItem -recurse | select-string  -pattern 'foo'
```

Example in ansible context:

```bash
ansible '~.*winserver' -m win_shell -a 'Get-ChildItem "c:/dirA/subdirB" -recurse | select-string  -pattern "foo.*bar"'
```
