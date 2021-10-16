---
title: creating a cd copy on macos
categories:
  - macos
  - copy cd
author: Oliver Gaida
version: 1
---

# {{ page.title }}

Wie erstelle ich eine Kopie einer CD unter Macos?

Das läuft in 2 Schritten:

1. Kopie als iso-Datei erstellen
2. iso auf leere CD brennen

## Requirements 

CD-Laufwerk zum Beispiel über USB 

Ich habe aus einem alten PC ein DVD-Brenner ausgebaut und die Anschlüsse eines alten externen Festplattengehäuses genutzt:

![https://raw.githubusercontent.com/ogaida/snippets/master/images/cd.jpg](https://raw.githubusercontent.com/ogaida/snippets/master/images/cd.jpg)

## ISO erstellen

```
ls -1 /Volumes
hdiutil makehybrid -iso -joliet -o ../test2.iso /Volumes/CDNAME/
Creating hybrid image...
....
```

