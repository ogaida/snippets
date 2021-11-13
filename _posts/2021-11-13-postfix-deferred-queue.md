---
title: deferred queue analysis
categories:
  - linux
  - postfix
author: Oliver Gaida
version: 1
---

# {{ page.title }}

## Top 10 der deferred queue abrufen:

```bash
postqueue -j | jq -r '.|select(.queue_name == "deferred")|.recipients[]|.delay_reason' | sort | uniq -c | sort -nr | head -10
```

## Detailierte Datensätze zu einem speziellen delay_reason anzeigen

hier habe ich als Grund "1.2.3.4 blocked" angegeben:

```bash
postqueue -j | jq -r --arg reason "1.2.3.4 blocked" '.|select(.queue_name == "deferred")|select(.recipients[]|.delay_reason|contains($reason))'
```



## als bash-functions 

```
function top10deferred_reasons(){
        postqueue -j | jq -r '.|select(.queue_name == "deferred")|.recipients[]|.delay_reason' | sort | uniq -c | sort -nr | head -10
}

function list_deferred_records_by_reason(){
        reason=$1
        postqueue -j | jq -r --arg reason "$reason" '.|select(.queue_name == "deferred")|select(.recipients[]|.delay_reason|contains($reason))'
}
```