---
title: "show active conncetions"
category: netstat
author: Oliver Gaida
version: 1
---

# Anzeigen der aktiven Netzwerkverbindungen

## Windows

cmd:

```
netstat -an
```

aktive Verbindungen nach Remote-Adressen gruppieren

powershell:

```
Get-NetTCPConnection | where {$_.state -like 'Established*' -or $_.state -like '*wait*'} | select RemoteAddress | sort | group RemoteAddress | select count,name | sort-object count -descending
```

## Linux

```
netstat -tapen
```

Gruppieren nach remote Adressen:

```
netstat -tapen | awk '{print $5}' | awk -F: '{print $1}' | sort | uniq -c | sort -nr
```
