---
title: "Ansible win_shell und win_copy Beispiele"
category: ansible
author: Oliver Gaida
version: 1
---

# Ansible win_shell und win_copy Beispiele

## Umgebungsvariablen ausgeben

```bash
ansible mywinserver -m win_shell -a '"set"  executable=cmd'
mywinserver | CHANGED | rc=0 >>
ALLUSERSPROFILE=C:\ProgramData
...
```

## ein Datei kopieren

```bash
ansible mywinserver -m win_copy -a 'src=myfile dest=C:\Users\Administrator\AppData\Local\Temp\'
mywinserver | CHANGED => {
    "changed": true,
    "checksum": "ea746b770384363e7dede33e503a11081bfd47ee",
    "dest": "'C:\\Users\\Administrator\\AppData\\Local\\Temp\\myfile'",
    "operation": "file_copy",
    "original_basename": "myfile",
    "size": 130,
    "src": "myfile"
}
```

## Den Inhalt einer Textdatei ausgeben

```bash
ansible mywinserver -m win_shell -a '"type C:\Users\Administrator\AppData\Local\Temp\myfile"   executable=cmd'
mywinserver | CHANGED | rc=0 >>
Line 1 of myfile
Line 2 of myfile
```
