---
title: "Cubie"
date: 2018-04-01T20:53:53+02:00
draft: true
---

* [Download Armbian](https://www.armbian.com/cubietruck/) ([mainline > legacy](https://docs.armbian.com/User-Guide_Getting-Started/#legacy-or-mainline))
* [Getting Started Docs](https://docs.armbian.com/User-Guide_Getting-Started/)

## First Steps

*This is basically a wrap-up of the most important steps from the Getting-Started Docs*

1. Login as `root/1234`
2. Connect to WiFi using `nmtui-connect SSID`

## Configure Keyboard

Run `sudo dpkg-reconfigure keyboard-configuration`
Modify `/etc/default/keyboard` accordingly (line `XKBLAYOUT`, change `us` to `de`)
Run `setupcon`

## Install Docker

As **root**, run `curl  https://get.docker.com | sh`
Then, as user `sudo usermod -aG docker mn`