---
title: "iptables - reduce number of concurrent connections"
categories:
  - iptables
  - linux
author: Oliver Gaida
version: 2
---

# iptables - reduce number of concurrent connections

the hint comes from [https://unix.stackexchange.com/questions/139285/limit-max-connections-per-ip-address-and-new-connections-per-second-with-iptable](https://unix.stackexchange.com/questions/139285/limit-max-connections-per-ip-address-and-new-connections-per-second-with-iptable)

add the rule:

```bash
iptables -A INPUT -p tcp --syn --dport 8878 -m connlimit --connlimit-above 2 --connlimit-mask 32 -j REJECT --reject-with tcp-reset
```

check the rules:

```bash
iptables -S INPUT
```

test the rule with three different web-browsers at the same time. see [my youtube video](https://youtu.be/zn6Gth1ELGk)

delete the rule

```bash
iptables -D INPUT -p tcp --syn --dport 8878 -m connlimit --connlimit-above 2 --connlimit-mask 32 -j REJECT --reject-with tcp-reset
iptables -S INPUT
ss -at | grep 8878
```

in case you want to log rejected connections you can just add the same iptables-rule with the logging parameters before, for example you can insert two rules:

```bash
iptables -A INPUT -p tcp --syn --dport 8878 -m connlimit --connlimit-above 2 --connlimit-mask 32 -j LOG --log-level 6 --log-prefix to-many-concurrent-connections
iptables -A INPUT -p tcp --syn --dport 8878 -m connlimit --connlimit-above 2 --connlimit-mask 32 -j REJECT --reject-with tcp-reset
```
