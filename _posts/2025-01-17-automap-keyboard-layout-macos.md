---
title: "automap keyboard-layout on macos"
category: macos
author: Oliver Gaida
version: 3
---

# automap keyboard-layout on macos

see [https://github.com/ohueter/autokbisw](https://github.com/ohueter/autokbisw)

switches the keyboard layout when the keyboard is used automaticly.

Requirement: needs xcode installed

- install xcode via appstore
- then on commandline

```bash
sudo xcodebuild -license accept
brew install ohueter/tap/autokbisw
brew services start autokbisw
```

allow access

![alt text](https://snippets.schnatzefatt.de/images/macos-kb-l-0.png)

![alt text](https://snippets.schnatzefatt.de/images/macos-kb-l-1.png)

```bash
autokblist clear
brew services stop autokbisw
brew services start autokbisw
# after mapping it looks like
autokbisw list
1. 2.4G Receiver-[9639-64103-CX-unknown]: enabled - Windows Tastatur, Deutsch (org.unknown.keylayout.WindowsTastaturDeutsch)
2. Magic Keyboard von Oliver-[76-671-Apple Inc.-88:4D:7C:E9:C4:8B]: enabled - ABC – QWERTZ (com.apple.keylayout.ABC-QWERTZ)
```