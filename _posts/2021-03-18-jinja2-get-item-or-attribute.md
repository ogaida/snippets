---
title: "jinja2 - get item or attribute"
category: jinja2
author: Oliver Gaida
version: 1
---

# jinja2 - get item or attribute

Worum geht es heute? Auf [https://jinja.palletsprojects.com/en/2.11.x/templates/#variables](https://jinja.palletsprojects.com/en/2.11.x/templates/#variables) wird
beschrieben, dass die Attribute und Items von Python-Objekte in Jinja2 auf 2 verschiedenen Wegen ausgelesen werden können, bezogen auf Objekt a mit Attribute oder Item b wäre das :

1. mit der Punkt-Notation: `a.b` für Attribute
2. mit der Item-Notation: `a["b"]` bei Dictionaries

Wie eben schon gesagt spielt das in Jinja2 keine Rolle, da intern ein Python-Objekt gleichzeitig kein Attribute und Dictionary Item sein dürfte.

Am besten veranschaulichen wir uns das an einem Beispiel. Ich definiere 2 Klassen:

```python
class K1:
  k1 = "Oliver ist schlau"

class K2:
  b = { "k1": 1,  "k2": 5 }
  c = K1
```

Das Attribute c der Klasse K2 beinhaltet eine Instanz der Klasse K1. Das Attribute b der Klasse K2 verweisst hingegen auf ein Dictionary. Folgende Ergebnisse in erhalte ich in Python:

```python
x.b["k1"] # => 1 
x.b.__getitem__('k1') # => 1
x.c.k1 # => 'Oliver ist schlau'
getattr(x.c, 'k1') # => 'Oliver ist schlau'
x.c["k1"]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'type' object is not subscriptable
```

Nun schauen wir uns die beiden Notation in Jinja2 an:

```python
from jinja2 import Template
template = Template('{{ x.b.k1 }}')
template.render(x=x) # => '1'
template = Template('{{ x.c.k1 }}')
template.render(x=x) # => 'Oliver ist schlau'
template = Template('{{ x.b["k1"] }}')
template.render(x=x) # => '1'
template = Template('{{ x.c["k1"] }}')
template.render(x=x) # => 'Oliver ist schlau'
```

In Jinja2 spielt es also keine Rolle ob man die Attribute oder Item-Syntax nimmt und ob ein Attribute oder Item abgefragt wird.

Quelle: [https://jinja.palletsprojects.com/en/2.11.x/templates/#variables](https://jinja.palletsprojects.com/en/2.11.x/templates/#variables)