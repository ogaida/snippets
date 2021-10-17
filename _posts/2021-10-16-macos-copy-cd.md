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

Das läuft in 5 Schritten:

1. mit der Musik.app die Dateien importieren
2. playlist erstellen
3. imporierte Dateien der playlist hinzufügen
4. playlist sortieren
5. playlist auf neue CD brennen

## Requirements 

CD-Laufwerk zum Beispiel über USB 

Ich habe aus einem alten PC ein DVD-Brenner ausgebaut und die Anschlüsse eines alten externen Festplattengehäuses genutzt:

![https://raw.githubusercontent.com/ogaida/snippets/master/images/cd.jpg](https://raw.githubusercontent.com/ogaida/snippets/master/images/cd.jpg)


## Weg der mir nicht gelungen ist:

ich hatte es mit `drutils burn -audio /path/to/mp3-files` brobiert. Hier ging jedoch die Reihenfolge durcheinander. Ich habe keine Möglichkeit gefunden, die Dateien unter `drutil` sortiert schreiben zu lassen.