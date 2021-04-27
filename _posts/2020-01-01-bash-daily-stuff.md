---
title:  "daily stuff"
category: bash
author: Oliver Gaida
version: 3
---

# Kommentare und leere Zeilen ausblenden

```bash
grep -vP '^(\s*#.*|\s*)$'
```

# In der `.bashrc` unterscheiden ob interactiv oder nicht

wenn ich mit git per ssh auf einen Account gehe, möchte ich keine Interaktionen wie spezielle Passworteingaben ausführen, deshalb habe ich folgende Abfrage entworfen:

```bash
if [ ! "${SSH_TTY}" = "" ] ||  pstree -ps | grep $$ | grep sudo > /dev/null
then
    echo "Wer bist Du?"
    read wer
    echo "Hallo $wer !"
fi
```