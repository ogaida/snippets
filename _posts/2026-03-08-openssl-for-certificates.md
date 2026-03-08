---
title:  wichtige openssl Befehle
categories:
- linux 
- certificates
author: Oliver Gaida
version: 1
---

## selbstsigniertes Zertifikat erzeugen

`openssl req -x509 -sha256 -noenc -days 365 -newkey rsa:2048 -keyout key.pem -out cert.pem`

## Zertifikat prüfen

`openssl x509 -in cert.pem -text -noout`

## Zertifikat und Key gegeneinander prüfen

Passen Zertifikat und Key zusammen?

```bash
function cert2key_match(){
    cert=$1
    key=$2
    if [ $(openssl x509 -modulus -noout -in $cert) == $(openssl rsa -modulus -noout -in $key) ]
    then
        echo cert and key belong to eachother
    else
        echo cert and key do not belong to eachother
    fi
}
cert2key_match c.pem k.pem 
cert and key belong to eachother
```

## Keys mit Passwörtern

### Passwort hinzufügen

`openssl rsa -in key.pem -out key_mit_pw.pem -aes256`

### Passwort vom Key entfernen

`openssl rsa -in key_mit_pw.pem -out key_ohne_pw.pem`

## Key und Zertifikat-Anfrage (CSR) erzeugen

mit interaktiver Eingabe alle benötigten Daten

`openssl req -nodes -new -newkey rsa:4096 -sha256 -out csr.pem -keyout key.pem`

## pfx Konvertierung

### von pem zu pfx

`openssl pkcs12 -export -out cert.pfx -inkey key.pem -in cert.pem -name name`

mit chain:

`openssl pkcs12 -export -out cert.pfx -inkey key.pem -in cert.pem -certfile chain.pem -name name`

### von pfx zu pem

`openssl pkcs12 -in cert.pfx -out fullchain.pem -nodes`