---
title: routing in macos
categories:
  - macos
  - routing
author: Oliver Gaida
version: 2
---

# {{ page.title }}

routing in macos - show routing tables, add a route etc.

## Routingtabelle anschauen

alle Eiträge inklusive IPv6

```
netstat -rn
```

Erklärung der Parameter:

- `-r` Routingtabelle anschauen
- `-n` Nummern anzeigen, bzw. IP-Adressen nicht zu Namen auflösen

nur IPv4 Einträge anschauen

```
netstat -rnf inet
```

`-f` filtert auf die angegebene Adressenfamilie. Möglich sind hier:

| Name  | Beschreibung            |
| ----- | ----------------------- |
| inet  | IPv4 Adressen           |
| inet6 | IPv6 Adressen           |
| unix  | AF_UNIX, lokale Sockets |

### Ausgabe filtern mit sed

Hier ein Beispiel, wie man nach ppp-Einträgen filtern kann:

```
netstat -rnf inet | gsed -n '4 {p};/ppp/ {p}'
```

### Route hinzufügen

Möchte man nun den Netzwerkverkehr ein privates Subnetz über ein spezielles Interface zwingen, so kann man eine entsprechende Route konfigurieren:

Ein Beispiel:

Anfragen zum Subnetz 192.168.10 sollen über ppp1 gehen:

```
sudo route add -net 192.168.10 -interface ppp1
```

alternativ geht auch:

```
networksetup -setadditionalroutes "my vpn xy" 192.168.10.0 255.255.255.0 192.168.1.1
```

Den hier verwendeten vpn Namen kann über folgendes Kommando ermitteln:

```
networksetup -listnetworkserviceorder
```

Falls man per Kommandozeile vorher noch die vpn-Verbindung aufbauen will, funktioniert das mit dem folgenden Befehl:

```
networksetup -connectpppoeservice "my vpn xy"
```