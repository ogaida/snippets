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

Original CD einlegen. 

Devices auf der Commandline Auflisten :

```
diskutil list
```

Ausgabe:

```
/dev/disk0 (internal, physical):                              .  MB
   #:                       TYPE NAME     r     4⁩       SIZE  TB   IDENTIFIER
....
/dev/disk5 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:        CD_partition_scheme Das Weihnachtspony ... *708.1 MB   disk5
   1:                      CD_DA                         66.8 MB    disk5s1
   2:                      CD_DA                         79.6 MB    disk5s2
   3:                      CD_DA                         59.2 MB    disk5s3
   4:                      CD_DA                         87.2 MB    disk5s4
   5:                      CD_DA                         93.2 MB    disk5s5
   6:                      CD_DA                         33.5 MB    disk5s6
   7:                      CD_DA                         61.6 MB    disk5s7
   8:                      CD_DA                         68.4 MB    disk5s8
   9:                      CD_DA                         34.0 MB    disk5s9
  10:                      CD_DA                         23.3 MB    disk5s10
  11:                      CD_DA                         58.8 MB    disk5s11
  12:                      CD_DA                         42.5 MB    disk5s12
```
