---
title:  "test different users and passwords for ssh login"
categories: 
  - bash
  - expect
author: Oliver Gaida
version: 3
---

# ssh testen mit verschiedenen Kombinationen von Username und Passwort

## Voraussetzungen

### Installation von expect

`apt install expect` auf ubuntu oder auf dem mac `brew install expect`

### Expect-Skript erstellen

`vim test_ssh_login`

```
#!/usr/bin/expect -f
set username [lindex $argv 0]
set password [lindex $argv 1]
set hostname [lindex $argv 2]
spawn ssh -oNumberOfPasswordPrompts=1  "${username}@${hostname}" "uname -a"
expect "assword:"
send "${password}\r"
interact
```

### Shellscript Anlegen

`vim make_login_test.sh`

```bash
#!/usr/bin/env bash

host=$1
for user in user1 user2 user3
do 
    for password in '123?!' '?!123'
    do 
        expect test_ssh_login "$user" "$password" $host | grep -i x86 > /dev/null && echo "user $user with password $password has been successful done"
    done
done
```

Ausführbar machen mit `chmod 750 make_login_test.sh`


## Test Ausführen
  
`./make_login_test.sh myserver`
