---
title:  "Conditionals in Ansible"
category: ansible
author: Oliver Gaida
version: 1
---

# Logische Operationen in Ansible

## Negation

```yaml
- shell: echo "This certainly isn't epic!"
  when: not epic
```

## Variable gesetzt?


```yaml
- shell: echo "I've got '{{ foo }}' and am not afraid to use it!"
  when: foo is defined

- fail: msg="Bailing out. this play requires 'bar'"
  when: bar is undefined
```

## Wert überprüfen

Adhoc-Kommando:

<!--{% raw %} -->

```bash
ansible localhost -m debug -a 'msg="{% if 1 == 1 %}{{ \"ja\"  }}{% else %}{{ \"nein\"  }}{% endif %}"'
localhost | SUCCESS => {
    "msg": "ja"
}
```

<!--{% endraw %} -->

## Substring ist enthalten

```yaml
- shell: echo "motd contains the word hi"
  when: motd_contents.stdout.find('hi') != -1
```

