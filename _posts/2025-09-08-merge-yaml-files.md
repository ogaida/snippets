---
title: merge yaml files
category: yaml
author: Oliver Gaida
version: 1
---

# merge yaml files

given a file `a.yml`:

```yaml
a: []
b: 1
c: 
- 4
- 5
```

create json with `jo`:

```bash
jo a="$(jo -a 12 17)" c="$(jo -a "a b" "c d")"
# => {"a":[12,17],"c":["a b","c d"]}
```

merge it:

```bash
jq -s '.[0] * .[1]' <(yq . a.yaml) <(jo a="$(jo -a 12 17)" c="$(jo -a "a b" "c d")")|yq -y .
```

gives:

```yaml
a:
  - 12
  - 17
b: 1
c:
  - a b
  - c d
```

a and c have been overwritten.