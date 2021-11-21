---
title: macos mail.app - Deaktivieren der Inline Attachments
categories:
  - macos
  - mail.app
author: Oliver Gaida
version: 3
---

# {{ page.title }}

## Das Problem

Wenn man in der Mail.app auf macos Bilder verschickt, werden diese in einer html formatierten Email versendet. Die Bilder sind dann im html eingefügt und nicht als Anhang in der Email verfügbar. Dadurch wird es für manch einen Empfänger nahezu unmöglich diese Bilder aus der Email zu speichern.

## Lösung

Voreinstellung der mail.app ändern.

### 1. Terminal öffnen

cmd-Taste + Leertaste drücken, terminal eingeben und ENTER.

### 2. Befehl ausführen

folgenden Befehl im Terminal mit cmd-Tast + v einfügen und ausführen (ENTER)

```bash
defaults write com.apple.mail DisableInlineAttachmentViewing -bool yes
```

## Rückgängig machen

Wem das nicht gefällt, der kann die Änderung mit 

```bash
defaults write com.apple.mail DisableInlineAttachmentViewing -bool false
```

wieder zurücksetzen.

# Screencast

Das ganze könnt ihr euch auch auf youtube anschauen unter: [https://youtu.be/vjkFPsUhCaE](https://youtu.be/vjkFPsUhCaE)