---
title: running checkmk mrpe checks in windows
categories:
  - windows
  - checkmk
author: Oliver Gaida
version: 4
---

# {{ page.title }}

Beispiele für checkmk mit mrpe unter Windows.

Den Screencast zum Beitrag findet ihr auf: [https://youtu.be/mVcZW0moi1A](https://youtu.be/mVcZW0moi1A)

## Nagios-Konventionen für nrpe

siehe [https://nagios-plugins.org/doc/guidelines.html#AEN200](https://nagios-plugins.org/doc/guidelines.html#AEN200)

## Umsetzung

Ergänzung in `C:\Program Files (x86)\checkmk\service\check_mk.yml`

```
mrpe:
    enabled: yes
    parallel: no
    timeout: 60
    config:
        - check = app_pool C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe C:\scripts\app_pool_test.ps1
        - check = dns_jolejo.de C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe C:\scripts\check_dns.ps1 8.8.8.8 jolejo.de
        - check = dns_berlin.de C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe C:\scripts\check_dns.ps1 8.8.8.8 berlin.de
        - check = windows_update_status C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe C:\scripts\check_windows_updates.ps1
```

Wichtig: keine Tabs verwenden. nur Leerzeichen...

## Test

output `C:\Program Files (x86)\checkmk\service>check_mk_agent.exe test`:

```
<<<mrpe>>>
(powershell.exe) app_pool 0 OK: All Websites and AppPools Running. | WebsitesRunning=1;0;0;0;1 AppPoolsRunning=2;0;0;0;2
(powershell.exe) dns_jolejo.de 0 OK: dns returned 45.132.246.103
(powershell.exe) dns_berlin.de 0 OK: dns returned 109.68.230.145
(powershell.exe) windows_update_status 1 Updates: 0 critical, 2 optional|critical=0;optional=2;hidden=0
<<<>>>
```