---
title: "iptables - reduce the number of global connections per second"
categories:
  - iptables
  - linux
author: Oliver Gaida
version: 1
---

# iptables - reduce the number of global connections per second

[screencast](https://youtu.be/qVsiC-CueaA)

add the rules:

```
iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A INPUT -p tcp -m tcp --dport 22 -j ACCEPT
iptables -A INPUT -p tcp --dport 8878 -m state --state NEW -m limit --limit 6/s --limit-burst 8 -j ACCEPT
iptables -A INPUT -j REJECT --reject-with icmp-port-unreachable
```

check the rules:

```bash
iptables -S INPUT
```

delete the rules:

```bash
iptables -D INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -D INPUT -p tcp -m tcp --dport 22 -j ACCEPT
iptables -D INPUT -p tcp --dport 8878 -m state --state NEW -m limit --limit 6/s --limit-burst 8 -j ACCEPT
iptables -D INPUT -j REJECT --reject-with icmp-port-unreachable
```

test the rules:

```bash
seq 1 50|while read a; do nc -z -w 1 192.168.2.250 8878 && echo "${a}: ok"||echo "${a}:failed"; done
```
