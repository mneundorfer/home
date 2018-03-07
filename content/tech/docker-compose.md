---
title: "First Steps: Docker Compose"
date: 2018-01-12T20:23:22+01:00
draft: true
tags: ["docker", "docker-compose"]
---

```yml
cloud:
  image: l3iggs/owncloud:daily
  ports: 
    - 80:80
    - 443:443
  volumes:
    - /oc-data:/usr/share/webapps/owncloud/data

vpn:
  image: kylemanna/openvpn

backup-home:
  image: linuxserver/duplicati

backup-oc:
  image: linuxserver/duplicati

backup-ovpn:
  image: linuxserver/duplicati
```