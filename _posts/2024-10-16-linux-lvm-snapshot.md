---
title:  lvm snapshot before critical changes
categories: 
  - linux 
  - lvm
author: Oliver Gaida
version: 1
---

# linux - lvm snapshot before critical changes

make most sense on physical machines, because on virtual machines in most cases it is easier to create a snapshot with the hypervisor toolset.

generell requirements: 
- enough space left on the the corrsponding volumegroup

## how it goes

my situation:

```bash
root@nbsy:~# lvs
  LV     VG  Attr       LSize  Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  lv-sys vg0 -wi-ao---- 20.00g
  test   vg0 -wi-a-----  1.00g
root@nbsy:~# df -h
Filesystem               Size  Used Avail Use% Mounted on
tmpfs                    1.6G  1.7M  1.6G   1% /run
/dev/mapper/vg0-lv--sys   20G  7.2G   12G  39% /
tmpfs                    7.8G     0  7.8G   0% /dev/shm
tmpfs                    5.0M     0  5.0M   0% /run/lock
/dev/sda1                1.1G  6.1M  1.1G   1% /boot/efi
/dev/sda3                590G   28K  560G   1% /data
tmpfs                    1.6G  4.0K  1.6G   1% /run/user/1000
root@nbsy:~#
```

### create snapshot

```bash
lvcreate -s -L 10G -n snap_initial /dev/vg0/lv-sys
```

### do not keep changes / delete everything and go back to the snapshot version 

```bash
# back to before-state:
lvconvert --merge /dev/vg0/snap_initial
# reboot the system
# refresh lvstate:
lvchange --refresh vg0
# create again the original snapshot, because after merging it was deleted
lvcreate -s -L 10G -n snap_initial /dev/vg0/lv-sys
```

### keep changes and do more testing

```bash
lvremove /dev/vg0/snap_initial
lvcreate -s -L 10G -n snap_initial /dev/vg0/lv-sys
```


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


