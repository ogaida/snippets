
# Ansible hello world

ein einfaches Playbook:

```yaml
- hosts:
  - lokal
  tasks:
    - name: Create a directory
      file: path=hello_world state=directory
    # jetzt schreibe ich eine sehr lange ZEILE und schaue, ob ich hier scrollen kann.
```

read about github-pages here [./README-jekyll](./README-jekyll)

# more

- [conditionals](./Conditionals.html)
- [windows](./windows.html)
- [bash](./bash.html)
- [regex](./regex.html)
- [jekyll](./jekyll.html)

Diese Seite findest Du auf [https://jekyll.schnatzefatt.de/](https://jekyll.schnatzefatt.de/)
