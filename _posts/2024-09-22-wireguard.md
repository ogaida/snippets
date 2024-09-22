---
title:  wireguard
categories: 
  - linux 
  - vpn
author: Oliver Gaida
version: 1
---

# Wireguard on linux - connect 2 clients behind a firewall

goal: 
- configure two clients and one server.
- both clients should be able to talk to each other.

## Installation

```bash
apt install wireguard
```

## Overview

![https://raw.githubusercontent.com/ogaida/snippets/master/images/wg1.png](https://raw.githubusercontent.com/ogaida/snippets/master/images/wg1.png)


helper aliases:

```bash
alias wg_conf_show="clear;echo $HOSTNAME; echo ''; grep -ivP '^(#|priva|endp|Presha)' w.conf |cat ; read dummy"
alias wg_restart="wg-quick down w;wg-quick up w"
alias wg_status="clear;echo $HOSTNAME; echo ''; wg |grep -v endp ; read dummy"
```

Client-1 :

```ini
[Interface]
Address = 10.0.0.101/32
```

Client-2 :

```ini
[Interface]
Address = 10.0.0.102/32
```

Server (%i is a placeholder for the devicename):

```ini
[Interface]
Address = 10.0.0.100/32
```

```bash
wg genkey > w_priv
wg-quick up w
wg set w private-key w_priv listen-port 1820
wg-quick save w
rm w_priv
wg_status
```

at this point take over the public keys into the commands below!

check wireguard.sc4y.de, was setup in my /etc/hosts only. it has not been setup in public dns:

```bash
ping -n wireguard.sc4y.de | perl -ne 's/\d+\.\d+\.\d+\.\d+/wireguard.sc4y.de/;print $_'
```

client 1:

```bash
wg set w peer <pubkey-server> endpoint wireguard.sc4y.de:1820 allowed-ips 10.0.0.100/32,10.0.0.102/32
wg-quick save w
```

client 2:

```bash
wg set w peer <pubkey-server> endpoint wireguard.sc4y.de:1820 allowed-ips 10.0.0.100/32,10.0.0.101/32
wg-quick save w
```

server:

```bash
wg set w peer <pubkey-client-1> allowed-ips 10.0.0.101/32
wg set w peer <pubkey-client-2> allowed-ips 10.0.0.102/32
wg-quick save w
sysctl -w net.ipv4.ip_forward=1
```

Remark: wireguard.sc4y.de does not exists, it  was only setup in /etc/hosts to aim the wireguardserver's public ip-address.

## Use Preshared Keys

sense: enrich the quality of encryption because, public and shared_key will be used to encrypt the data.
so put a preshared key into the peer sections...

Attention: 2 corresponding peers (i.g. peer <-> server) must use the same pre-shared key!

on all:

```bash
# shut off tmux sync
# on server:
nc -l 51820 > preshared-key-of-cli-1
# on client-1:
wg genpsk > preshared_key_file
sha1sum preshared_key_file
cat preshared_key_file | nc 10.0.0.100 51820 
<ctrl-c>
wg set w peer <pubkey-server> preshared-key preshared_key_file
wg-quick save w
# on server:
sha1sum preshared-key-of-cli-1
nc -l 51820 > preshared-key-of-cli-2
# on client-2:
wg genpsk > preshared_key_file
sha1sum preshared_key_file
cat preshared_key_file | nc 10.0.0.100 51820 
<ctrl-c>
wg set w peer <pubkey-server> preshared-key preshared_key_file
wg-quick save w
# on server:
sha1sum preshared-key-of-cli-2
wg set w peer <pubkey-client-1> preshared-key preshared-key-of-cli-1
wg set w peer <pubkey-client-2> preshared-key preshared-key-of-cli-2
wg-quick save w
# set on tmux sync
wg_status
ping 10.0.0.100
ping 10.0.0.101
ping 10.0.0.102
```


