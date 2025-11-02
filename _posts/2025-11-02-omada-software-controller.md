---
title:  omada software controller on ubuntu noble 24.04
category: omada
author: Oliver Gaida
version: 1
---

```bash
apt install curl
# add repo for mongodb
curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg --dearmor
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
sudo apt update
# jre is required
sudo apt install openjdk-17-jre-headless
# list of controller versions: https://support.omadanetworks.com/de/product/omada-software-controller/?resourceType=download
wget https://static.tp-link.com/upload/software/2025/202508/20250802/omada_v5.15.24.19_linux_x64_20250724152622.deb
sudo apt install ./omada_v5.15.24.19_linux_x64_20250724152622.deb   
```