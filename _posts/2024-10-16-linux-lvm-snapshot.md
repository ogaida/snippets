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

