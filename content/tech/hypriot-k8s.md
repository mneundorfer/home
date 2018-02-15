---
title: "RPi3, Hypriot & Kubernetes"
date: 2018-02-11T22:06:11+01:00
draft: true
tags: ["rpi", "hypriot", "docker"]
---

Base Link: [Hypriot-Docs](https://blog.hypriot.com/post/setup-kubernetes-raspberry-pi-cluster/)

# Install Hypriot

* [Hypriot-Releases](https://github.com/hypriot/image-builder-rpi/releases)
* Use [Rufus](https://rufus.akeo.ie/) to flash

# Setup RPi

## Network Connectivity

WLAN is not active by default (`wlan0 Interface doesn't support scanning : Network is down` when `sudo iwlist wlan0 scan`).

```bash
# bring it up...
sudo ifconfig wlan up
```

```bash
# credentials
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf

network={
    ssid="SSID"
    psk="PASSWORD"
}
```

```bash
sudo nano /etc/network/interfaces

# if configuration
#auto eth0
#  iface eth0 inet dhcp

auto wlan0
  iface wlan0 inet dhcp
  wpa_conf /etc/wpa_supplicant/wpa_supplicant.conf

# avoid network disconnects due to power save config
pre-up iw dev wlan0 set power_save off
post-down iw dev wlan0 set power_save on
```

```bash
# restart
sudo ifdown wlan0 && sudo ifup wlan0
```