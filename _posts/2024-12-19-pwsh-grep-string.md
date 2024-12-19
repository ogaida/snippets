---
title: "powershell - search string recursive in folder "
category: powershell
author: Oliver Gaida
version: 1
---

# powershell - search string recursive in folder

```powershell
Get-ChildItem -recurse | select-string  -pattern 'foo'
```
