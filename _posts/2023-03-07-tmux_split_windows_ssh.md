---
title:  "how to create multiple ssh connections in one new tmux session"
category: tmux
author: Oliver Gaida
version: 1
---

# how to create multiple ssh connections in one new tmux session

```bash
function new-tmux-session(){
    # Beispiel Aufruf:
    #   new-tmux-session 0 5 "bash -c 'echo " " && sleep 100'" testsession 3
    start=$1
    end=$2
    prefix=$3
    suffix=$4
    sessionname=$5
    filluplength=${6:-"2"}
    tmux new-session -d -s $sessionname -n $sessionname -d "${prefix}$(printf "%0${filluplength}s" $start)${suffix}"
    seq -f"%0${filluplength}g" $(($start + 1)) $end | while read i
    do  
        tmux split-window -t $sessionname "${prefix}${i}${suffix}"
        tmux select-layout -t $sessionname even-vertical
    done
}

# connect to 4 different dbservers : dbserver0.myhost.local - dbserver3.myhost.local
function new-tmux-session-my_dbserver(){ new-tmux-session 0 3 "ssh dbserver" ".myhost.local" my_dbserver 1; }
```

