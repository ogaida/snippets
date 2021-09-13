---
title: "show active conncetions"
category: netstat
author: Oliver Gaida
version: 6
---

# Anzeigen der aktiven Netzwerkverbindungen

## Windows

cmd:

```cmd
netstat -an
```

aktive Verbindungen nach Remote-Adressen gruppieren

powershell:

```powershell
Get-NetTCPConnection | where {$_.state -like 'Established*' -or $_.state -like '*wait*'} `
  | select RemoteAddress | sort | group RemoteAddress | select count,name ` 
  | sort-object count -descending
```

Wenn man stattdessen nur die Anzahl der established und wait-Verbindungen zählen möchte, genügt folgendes Kommando:

```powershell
(Get-NetTCPConnection | where {$_.state -like 'Established*' -or $_.state -like '*wait*'} ).count
```

## Linux

```bash
netstat -tapen
```

Gruppieren nach remote Adressen:

```bash
netstat -tapen | grep -iP  '(time_wait|establ|verbunden)' | awk '{print $5}' | awk -F: '{print $1}' | sort | uniq -c | sort -nr
```

Wenn man stattdessen nur die Anzahl der established und wait-Verbindungen zählen möchte, genügt folgendes Kommando:

```bash
netstat -tapen | grep -iP  '(time_wait|establ|verbunden)' | wc -l
```
