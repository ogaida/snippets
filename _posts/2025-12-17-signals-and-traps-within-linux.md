---
title:  signals and traps - testscript
category: linux 
author: Oliver Gaida
version: 5
---

Hier das Bash-Skript das ich in meinem Screencast zu Signals und Traps verwendet habe:

```bash
#!/usr/bin/env bash

echo "meine Prozessnummer ist: "$$
echo $$ > /tmp/trap_test_pid

# SIGHUP
trap "printf '\n';echo mir wurde gerade ein SIGHUP Signal geschickt, danke." 1
# SIGTERM
trap "printf '\n';echo mir wurde gerade ein SIGTERM Signal geschickt, danke.; exit 0" 15
# SIGINT / CTRL-C
trap "printf '\n';echo mir wurde gerade ein SIGINT Signal geschickt, danke.; exit 1" 2
# SIGKILL
trap "printf '\n';echo mir wurde gerade ein SIGKILL Signal geschickt, danke." 9

while true
do
    printf .
    sleep 1
done
```

siehe auch:

{% include youtube.html id="4UC9PQbfnc4" %}
