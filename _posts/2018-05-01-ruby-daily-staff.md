---
title:  "daily ruby stuff"
category: ruby
author: Oliver Gaida
version: 1
---

# Ruby

## keine Dokumentation bei `gem install` erstellen

Folgende Zeile in die Datei `~/.gemrc` einfügen:

```
gem: --no-document
```

## Dateieigeschaften ausgeben

```ruby
Dir["*"].each do |a|
  puts "#{a}:#{File.stat(a).size}"
end
```
