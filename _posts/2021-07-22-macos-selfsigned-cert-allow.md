---
title: selfsigned certificate allow usage
categories:
  - macos
  - certificates
author: Oliver Gaida
version: 1
---

# {{ page.title }}

you can not use selfsigned certificates on mac by default. How to change this?

## solution

### 1. get the certificate as file

```bash
dom=mydomainname.com
echo | openssl s_client -showcerts -servername ${dom} -connect ${dom}:443 2> /dev/null > mydom.pem
```

Now you have the cert on your disc.

### 2. open certificate in your keystore

double click the mydom.pem file. then the keystore app will open

### 3. trust the certificate

double click the certificate in your keystore. 

in the new window go on trust. then choose always trust. Then close this window and accept the change by authorize it with your admin credentials.