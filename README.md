
Das ist ein simples Playbook-Beispiel:

```yaml
- hosts:
  - lokal
  tasks:
    - name: Create a directory
      file: path=hello_world state=directory
    # jetzt schreibe ich eine sehr lange ZEILE und schaue, ob ich hier scrollen kann.
```

