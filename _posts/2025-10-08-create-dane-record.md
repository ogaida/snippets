---
title: DNS - create dane record
category: dns
author: Oliver Gaida
version: 1
---


```bash
function create_tlsa_record_from_web(){
    dom=$1
    port=$2
    starttls=${3:-""} # "-starttls pop3" oder "-starttls smtp" 
    echo | openssl s_client -connect ${dom}:$port $starttls 2> /dev/null \
        |openssl x509 -outform DER | openssl sha256 | cut -d'=' -f2 \
        | awk -v dom=$dom -v port=$port '{printf "_%s._tcp.%s. 600 TLSA 3 0 1 %s\n", port, dom, $NF}'
}
```

```bash
function create_tlsa_record_from_certfile(){
    dom=$1
    port=$2
    file=$3
    openssl x509 -in $file -outform DER | openssl sha256 | cut -d'=' -f2 \
        | awk -v dom=$dom -v port=$port '{printf "_%s._tcp.%s. 600 TLSA 3 0 1 %s\n", port, dom, $NF}'
}
```
