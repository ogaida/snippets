---
title: "powershell - get and set environment variables"
category: powershell
author: Oliver Gaida
version: 1
---

# powershell - get and set environment variables

```powershell
$userenv = [System.Environment]::GetEnvironmentVariable("Path", "User")
[System.Environment]::SetEnvironmentVariable("PATH", $userenv + ";C:\Users\Administrator\Ubuntu", "User")
```