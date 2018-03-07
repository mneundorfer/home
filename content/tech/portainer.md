---
title: "Portainer"
date: 2018-02-17T22:46:19+01:00
draft: false
tags: ["rpi", "docker", "portainer"]
---

## Setup Portainer

```bash
docker volume create portainer_data
docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portai
```

## Enable Docker API for Remote Access

(obviously only relevant for systems other than the one where Portainer is running on)

```bash
sudo vi /lib/systemd/system/docker.service

# Modify the line that starts with ExecStart to look like this:
ExecStart=/usr/bin/docker daemon -H fd:// -H tcp://0.0.0.0:4243

systemctl daemon-reload

sudo service docker restart

curl http://localhost:4243/version
```