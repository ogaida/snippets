---
title: "Ansible Jinja2 Arithmetic Operations"
categories: 
  - ansible
  - jinja2
author: Oliver Gaida
version: 1
---

# Ansible Jinja2 Arithmetic Operations

Jinja2 ist ja das Templating-System von Ansible. Von Zeit zu Zeit muss man hier auch mal rechnen. Hier demonstriere ich grundlegende Operationen, die da weiterhelfen.

Ich werde eine Shell-Funktion schreiben, die uns arithmetische Funktionen in Jinja2 interpretiert. Dazu vernwenden wir das Python Module j2cli.

## j2cli

Installation:

```bash
python -m pip install j2cli
```

Test

```bash
j2 <(echo "{{ 3 * 4 }}")
12
```

## Test-Daten 

Ich erzeuge ein Json-File, das uns als Input für die arithmetischen Operationen dient. Die Datei `ops.json` enthalte folgende Daten:

```json
[
  {
    "op": "Addition",
    "sample": "4 + 5"
  },
  {
    "op": "Substraktion",
    "sample": "5 - 4"
  },
  {
    "op": "Multiplikation",
    "sample": "5 * 4"
  },
  {
    "op": "Division",
    "sample": "4 / 5"
  },
  {
    "op": "Division ohne Rest",
    "sample": "8 // 5"
  },
  {
    "op": "Modulo",
    "sample": "8 % 5"
  },
  {
    "op": "Quadratwurzel",
    "sample": "16 ** (1/2)"
  },
  {
    "op": "dritte Wurzel",
    "sample": "27 ** (1/3)"
  },
  {
    "op": "Exponentialfunktion",
    "sample": "3 ** 3"
  },
  {
    "op": "absulter Wert",
    "sample": "-2 | abs"
  },
  {
    "op": "Konvertierung zu ganzer Zahl",
    "sample": "-1.23 | int"
  },
  {
    "op": "Runden",
    "sample": "-1.23 | round"
  },
  {
    "op": "Runden auf erste Nachkommastelle",
    "sample": "-1.23 | round(1)"
  },
  {
    "op": "Abrunden",
    "sample": "5.7 | round(0,'floor') | int"
  },
  {
    "op": "Aufrunden",
    "sample": "5.2 | round(0,'ceil') | int"
  },
  {
    "op": "String verdoppeln",
    "sample": "' 4.5 ' * 2"
  },
  {
    "op": "String zu Float konvertieren und verdoppeln",
    "sample": "(' 4.5 ' | float) * 2"
  }
]

```

## jinja2 bash function

`j2` ist in unserem Fall etwas umständlich im Verarbeiten unseres Inputs, deshalb baue ich einen kleinen wrapper drumherum.

```bash
function jinja2(){
    string=$1
    j2 <(echo "{{ $string }}")
}
export -f jinja2
```

Test:

```bash
jinja2 "4 + 5"
9
```

## Test-Daten aufbereiten

nun verwende ich `jq`, um unsere Testdaten in jinja2-wrapper konforme Aufrufe umzubauen: 

```bash
jq -r '.[]|"echo \"" + .op + ": " + .sample + " = $(jinja2 \"" +.sample + "\")\"" ' ops.json
echo "Addition: 4 + 5 = $(jinja2 "4 + 5")"
echo "Substraktion: 5 - 4 = $(jinja2 "5 - 4")"
echo "Multiplikation: 5 * 4 = $(jinja2 "5 * 4")"
echo "Division: 4 / 5 = $(jinja2 "4 / 5")"
echo "Division ohne Rest: 8 // 5 = $(jinja2 "8 // 5")"
echo "Modulo: 8 % 5 = $(jinja2 "8 % 5")"
echo "Quadratwurzel: 16 ** (1/2) = $(jinja2 "16 ** (1/2)")"
echo "dritte Wurzel: 27 ** (1/3) = $(jinja2 "27 ** (1/3)")"
echo "Exponentialfunktion: 3 ** 3 = $(jinja2 "3 ** 3")"
echo "absulter Wert: -2 | abs = $(jinja2 "-2 | abs")"
echo "Konvertierung zu ganzer Zahl: -1.23 | int = $(jinja2 "-1.23 | int")"
echo "Runden: -1.23 | round = $(jinja2 "-1.23 | round")"
echo "Runden auf erste Nachkommastelle: -1.23 | round(1) = $(jinja2 "-1.23 | round(1)")"
echo "Abrunden: 5.7 | round(0,'floor') | int = $(jinja2 "5.7 | round(0,'floor') | int")"
echo "Aufrunden: 5.2 | round(0,'ceil') | int = $(jinja2 "5.2 | round(0,'ceil') | int")"
echo "String verdoppeln: ' 4.5 ' * 2 = $(jinja2 "' 4.5 ' * 2")"
echo "String zu Float konvertieren und verdoppeln: (' 4.5 ' | float) * 2 = $(jinja2 "(' 4.5 ' | float) * 2")"
```

Nun das ganze in der Bash ausführen:

```bash
bash <(jq -r '.[]|"echo \"" + .op + ": " + .sample + " = $(jinja2 \"" +.sample + "\")\"" ' ops.json)
Addition: 4 + 5 = 9
Substraktion: 5 - 4 = 1
Multiplikation: 5 * 4 = 20
Division: 4 / 5 = 0.8
Division ohne Rest: 8 // 5 = 1
Modulo: 8 % 5 = 3
Quadratwurzel: 16 ** (1/2) = 4.0
dritte Wurzel: 27 ** (1/3) = 3.0
Exponentialfunktion: 3 ** 3 = 27
absulter Wert: -2 | abs = 2
Konvertierung zu ganzer Zahl: -1.23 | int = -1
Runden: -1.23 | round = -1.0
Runden auf erste Nachkommastelle: -1.23 | round(1) = -1.2
Abrunden: 5.7 | round(0,'floor') | int = 5
Aufrunden: 5.2 | round(0,'ceil') | int = 6
String verdoppeln: ' 4.5 ' * 2 =  4.5  4.5
String zu Float konvertieren und verdoppeln: (' 4.5 ' | float) * 2 = 9.0
```

siehe auch [https://jinja.palletsprojects.com/en/2.11.x/templates/#maths](https://jinja.palletsprojects.com/en/2.11.x/templates/#maths)

