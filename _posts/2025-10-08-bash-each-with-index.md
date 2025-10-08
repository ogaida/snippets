---
title: bash - each with index
category: bash
author: Oliver Gaida
version: 2
---

```bash
arr=(ab cd xy)
for i in "${!arr[@]}"
	do echo "at index $i there is value ${arr[$i]}"
done
# output:
at index 0 there is value ab
at index 1 there is value cd
at index 2 there is value xy
```
