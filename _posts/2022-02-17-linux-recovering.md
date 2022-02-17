---
title: recovering linux with a livecd or other linux boot disk
categories:
  - linux
author: Oliver Gaida
version: 1
---

# {{ page.title }}

Im Prinzip fasse ich hier die Hinweise von [https://wiki.ubuntuusers.de/chroot/Live-CD/](https://wiki.ubuntuusers.de/chroot/Live-CD/) zusammen.

## booten

Entweder mit einer linux-live-cd auf usb oder einem anderen linux-boot-medium.

## recover

nach dem Booten schaut man als root User mit `fdisk -l` oder `parted -l` an, wo die defekte Partition liegt. Als Beispiel nehmen wir `/dev/sdc2`.

- mounten mit `mount /dev/sdc2 /mnt`
- Gerätedateien einbinden:

```bash
for dir in /dev /dev/pts /proc /sys /run
do 
  mount --bind $dir /mnt$dir
done 
```

- in das defekte System wechseln: `chroot /mnt /bin/bash`

Danach befindet man sich im System das man nun reparieren kann, zum Beispiel Änderungen an der `/etc/fstab` vornehmen etc.

Viel Erfolg!