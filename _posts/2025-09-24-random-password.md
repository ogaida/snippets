---
title: create a random password with the length of 20
category: bash
author: Oliver Gaida
version: 1
---

i use a bit perl:

`shuf -n 20 <(seq 33 126|grep -v '^(34|39)$')|perl -ne 'chomp;print chr($_);END{print "\n"}'`