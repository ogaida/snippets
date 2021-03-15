---
title: "jinja2 specials"
category: jinja2
author: Oliver Gaida
version: 1
---

# jinja2 specials

Vorbemerkung:

die verwendete `jinja2` Funktion erläutere ich in [https://snippets.schnatzefatt.de/ansible/jinja2/2021/03/14/Ansible-Jinja-Arithmetic.html](https://snippets.schnatzefatt.de/ansible/jinja2/2021/03/14/Ansible-Jinja-Arithmetic.html)

## Konvetierung in Integer

Strings lassen sich mit der Funktion `int` in Integer konvertieren. Hier einige Beispiele:

```bash
$ jinja2 "'0o77' | int(base=8)"
63
$ jinja2 "'001111' | int(base=2)"
15
$ jinja2 "'0xff' | int(base=16)"
255
$ jinja2 "'12.5' | int(base=10)"
12
$ jinja2 "'12.5' | int"
12
```

## Test ob wahr oder falsch

```bash
$ jinja2 " (1==1) is true"
True
$ jinja2 " (1!=1) is false"
True
```

## Teste ob Variable definitert ist

```bash
$ jinja2 "v is defined"
False
$ jinja2 "v is not defined"
True
```

## Teste ob Wert boolean ist

```bash
$ jinja2 "True is boolean"
True
$ jinja2 "False is boolean"
True
```

## Teste auf Teilbarkeit

```bash
$ jinja2 "4 is divisibleby(2)"
True
$ jinja2 "4 is divisibleby(3)"
False
```

## Test auf Gleichheit

```bash
$ jinja2 "False is eq false"
True
$ jinja2 "2 is eq ('2'|int)"
True
```

## Teste ob ein Wert escaped ist

```bash
$ jinja2 "'&' | escape"
&amp;
$ jinja2 "('&' | escape) is escaped"
True
```

## Teste ob ein Integer-Wert gerade ist

```bash
$ jinja2 "1 is even"
False
$ jinja2 "-2 is even"
True
```

Quelle: [https://jinja.palletsprojects.com/en/2.11.x/templates/#list-of-builtin-tests](https://jinja.palletsprojects.com/en/2.11.x/templates/#list-of-builtin-tests)