---
title: incus - storage volumes
category: incus
author: Oliver Gaida
version: 1
---

# incus - storage volumes creation and deletion

we have a vm with name i1 and a storage pool with the name default.

`incus launch images:ubuntu/noble/cloud t --vm`

## show current state

`incus storage volume list default`

## create a storage volume on commandline

syntax: `incus storage volume create [<remote>:]<pool> <volume> [key=value...] [flags]`

create a storage with content-type block:

`incus storage volume create default  t-linstore  --type=block size=100GiB`


## attach the storage volume on commandline

syntax: `incus storage volume attach [<remote>:]<pool> <volume> <instance> [<device name>] [<path>] [flags]`

`incus storage volume attach default t-linstore i1`
