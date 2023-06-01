---
title: "powershell - tail -f file | grep"
category: powershell
author: Oliver Gaida
version: 1
---

# powershell - tail -f file | grep

```powershell
Get-Content -path '.\mylogfile.log' -wait  | select-string -pattern error
```
