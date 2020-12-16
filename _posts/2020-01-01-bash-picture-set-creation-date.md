---
title:  "set creationdate of file from EXIF-Attributes"
category: 
  - bash
  - exiftool
author: Oliver Gaida
---

# Dateidatum auf das originale Erstellungsdatum/Änderungsdatum des Bildes bzw. Videos ändern

Voraussetzung: 

Das exiftool ist installiert.

In den Ordner mit den Bilder und Videos wechseln und dann:

```bash
find . -type f | while read f 
do
  create_date=$(exiftool "$f" | grep -P '^Create Date\s+:' | head -1  | awk '{print $4":"$5}')
  date=$(date -jf "%Y:%m:%d:%H:%M:%S" $create_date +%Y%m%d%H%M.%S)
  touch -t $date "$f"
done
```

Die Konstruktion `find . -type f | while read f` macht sich gut, falls Leerzeichen in Pfad sind.
