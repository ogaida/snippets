---
title: "macos installer download" 
category: macos
author: Oliver Gaida
version: 1
---

# macos installer download

auf eine Big Sur folgendes ausführen:

```bash
$ sudo /usr/sbin/softwareupdate --list-full-installers
Finding available software
Software Update found the following full installers:
* Title: macOS Big Sur, Version: 11.2.3, Size: 12211077798K
* Title: macOS Big Sur, Version: 11.2.2, Size: 12200254955K
* Title: macOS Big Sur, Version: 11.2.1, Size: 12199403070K
* Title: macOS Catalina, Version: 10.15.7, Size: 8248985973K
* Title: macOS Catalina, Version: 10.15.7, Size: 8248854894K
* Title: macOS Catalina, Version: 10.15.6, Size: 8248781171K
* Title: macOS Mojave, Version: 10.14.6, Size: 6038419486K
* Title: macOS High Sierra, Version: 10.13.6, Size: 5221689433K
$ sudo /usr/sbin/softwareupdate --fetch-full-installer --full-installer-version 11.2.3 --verbose
Scanning for 11.2.3 installer
Installing: 14.0%
```

dann herunterladen:

```bash
$ sudo /usr/sbin/softwareupdate --fetch-full-installer --full-installer-version 11.2.3 --verbose
Scanning for 11.2.3 installer
Installing: 90.0%
Install finished successfully
$ cd /Applications/
$ ls -ld Inst*
drwxr-xr-x  3 root  wheel  96 16 Mär 15:40 Install macOS Big Sur.app
```

Quelle: [https://www.jamf.com/de/blog/installieren-sie-macos-mit-nur-einem-klick-neu/]{https://www.jamf.com/de/blog/installieren-sie-macos-mit-nur-einem-klick-neu/}