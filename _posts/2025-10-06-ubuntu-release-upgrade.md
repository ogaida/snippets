---
title: ubuntu release upgrade
category: ubuntu
author: Oliver Gaida
version: 1
---

## Vorbereitung

```bash
apt clean all
apt update
apt dist-upgrade
reboot
apt autoremove --purge
```

## release upgrade 

```bash
cat /etc/*release|grep focal > /dev/null && sed -i 's/focal/jammy/' /etc/apt/sources.list
cat /etc/*release|grep jammy > /dev/null && sed -i 's/jammy/noble/' /etc/apt/sources.list
apt clean all
apt update
apt full-upgrade
# falls ein Paket nicht deinstalliert werden kann,
# 	rausfinden warum das pre remove script fehlschlägt:
	/var/lib/dpkg/info/<package>.prerm remove
# 	oder einfach behalten mit:
	apt-mark hold <package>
	apt full-upgrade
reboot
# Paket locking wieder aufheben:
	apt-mark hold <package>
```