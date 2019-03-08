## Einträge aus einer Textdatei entfernen

```yaml
  - name: Server aus hosts Datei entfernen
    win_lineinfile:
      path: 'C:/mypath/123/filename'
      regexp: "(?i:({{ item }}))"
      state: absent
    with_items:
      - string1
      - string2
```

#### Erläuterungen dazu

1. Warum `(?i:...)` ?

Im Default werden die Regulären Ausdrücke case-sensitiv gesucht. Mit `?i:` kann man den ignorecase aktivieren.

Die Details dazu sind auf der entsprechenden Microsoftseite erläutert,
also [hier](https://docs.microsoft.com/en-us/dotnet/standard/base-types/regular-expression-language-quick-reference). 

2. Warum wird im Pfad ´/´ und kein ´\´ verwendet?

Das win_lineinfile Module ersetzt intern die `/` im Pfad durch `\`, dadurch funktioniert das schon mal. Ein `\`-Zeichen dient sehr
oft dem maskieren von speziellen Zeichen. Die hier verwendete Variante schliesst also aus, dass sonderbare Dinge passieren.

[HOME](./)
