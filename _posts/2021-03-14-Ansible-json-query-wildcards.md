---
title: "Ansible json_query mit wildcards"   
categories:
  - ansible
  - json
author: Oliver Gaida
version: 1
---

# Ansible json_query mit wildcards  

Nehmen wir einmal an uns interessieren die Versionen der Pakete, die in der Datei `package-lock.json` gelistet sind. Dann können wir das mit dem
folgenden Ansible-adhoc-Kommando ermitteln:

<!--{% raw %} -->

```bash
ansible localhost -m debug -a "msg={{ lookup('file', 'package-lock.json') | from_json | json_query('dependencies.*.version') }}" | head -10
localhost | SUCCESS => {
    "msg": [
        "1.3.1",
        "2.20.0",
        "5.11.0",
        "1.2.4",
        "1.0.12",
        "1.1.3",
        "1.0.6",
        "1.0.7",
```

<!--{% raw %} -->

Der Inhalte der Datei `package-lock.json` sieht dabei wie folgt aus:

```bash
head -20 package-lock.json
{
  "requires": true,
  "lockfileVersion": 1,
  "dependencies": {
    "colors": {
      "version": "1.3.1",
      "resolved": "https://registry.npmjs.org/colors/-/colors-1.3.1.tgz",
      "integrity": "sha512-jg/vxRmv430jixZrC+La5kMbUWqIg32/JsYNZb94+JEmzceYbWKTsv1OuTp+7EaqiaWRR2tPcykibwCRgclIsw=="
    },
    "commander": {
      "version": "2.20.0",
      "resolved": "https://registry.npmjs.org/commander/-/commander-2.20.0.tgz",
      "integrity": "sha512-7j2y+40w61zy6YC2iRNpUe/NwhNyoXrYpHMrSunaMG64nRnaf96zO/KMQR4OyN/UnE5KLyEBnKHd4aG3rskjpQ=="
    },
    "d3": {
      "version": "5.11.0",
      "resolved": "https://registry.npmjs.org/d3/-/d3-5.11.0.tgz",
      "integrity": "sha512-LXgMVUAEAzQh6WfEEOa8tJX4RA64ZJ6twC3CJ+Xzid+fXWLTZkkglagXav/eOoQgzQi5rzV0xC4Sfspd6hFDHA==",
      "requires": {
        "d3-array": "1",
```

Wie kommt man auf diesen Filter? 

`json_query` verwendet jmespath, um die passenden Filter auszutesten bietet sich der JMESPath Terminal an, siehe [hier](https://github.com/jmespath/jmespath.terminal).

Installieren mit:

```bash
pip install jmespath-terminal
```

In unserem Fall können wir dann die Datei `package-lock.json` in den JMESPath Terminal mit dem folgenden Befehl laden:

```bash
jpterm package-lock.json
```

Um die Version des `colors` Paketes anzeigen zu lassen, setzen wir den Filter auf `dependencies.colors.version`. Danach `colors` durch `*` ersetzen und wir haben die Vorlage
für unser Ansible-adhoc-Kommando.