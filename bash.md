[HOME](./)

# Kommentare und leere Zeilen ausblenden

```bash
grep -vP '^(\s*#.*|\s*)$'
```

# zufällig Subtraktionsaufgaben generieren

```bash
$ for a in $(seq 10); do paste -d '-=' <(seq 8704 -29 1454) <(seq 613 12 3613) <(seq 8091 -41 -2179) | sed -n $(( RANDOM % 250 ))p; done
3658-2701=957
1541-3577=-2036
7457-1129=6328
4528-2341=2187
6761-1417=5344
7051-1297=5754
1570-3565=-1995
7863-961=6902
6152-1669=4483
6587-1489=5098
```

# Dateidatum auf das originale Erstellungsdatum/Änderungsdatum des Bilder bzw. Videos ändern

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



[HOME](./)
