---
title: "iptables - reduce number of connections per second and per ipaddress"
categories:
  - iptables
  - linux
author: Oliver Gaida
version: 1
---

# iptables - reduce number of connections per second and per ipaddress

you can see a screencast of that on [https://youtu.be/ODMQ6XAC_oM](https://youtu.be/ODMQ6XAC_oM)

the hint comes from [https://snippets.bentasker.co.uk/page-2010021645-Rate-limiting-connections-with-iptables-and-hashlimit-BASH.html](https://snippets.bentasker.co.uk/page-2010021645-Rate-limiting-connections-with-iptables-and-hashlimit-BASH.html)

add the rules:

```
iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A INPUT -p tcp -m tcp --dport 22 -j ACCEPT
iptables -A INPUT -p tcp --dport 8878 -m conntrack --ctstate NEW -m hashlimit --hashlimit-mode srcip --hashlimit-upto 5/sec --hashlimit-burst 5 --hashlimit-name per_ip_conn_rate_limit -j ACCEPT   
iptables -A INPUT -j REJECT --reject-with icmp-port-unreachable
```


check the rules:

```bash
iptables -S INPUT
```

delete the rules:

```bash
iptables -S INPUT
iptables -D INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -D INPUT -p tcp -m tcp --dport 22 -j ACCEPT
iptables -D INPUT -p tcp --dport 8878 -m conntrack --ctstate NEW -m hashlimit --hashlimit-mode srcip --hashlimit-upto 5/sec --hashlimit-burst 5 --hashlimit-name per_ip_conn_rate_limit -j ACCEPT   
iptables -D INPUT -j REJECT --reject-with icmp-port-unreachable
```

test the rules:

```bash
seq 1 30|while read a; do nc -z -w 1 192.168.2.250 8878 && echo "${a}: ok"||echo "${a}:failed"; done
```
