---
title: "Wireguard Split Tunelling"
date: 2025-07-23T09:45:20+05:00
description: ""
slug: "/wireguard-split-tunelling/"
# cover:
#     image: "<image path/url>"
#     alt: "<alt text>"
#     caption: "<text>"
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
draft: false
tags: [Networking,Linux]
categories: Linux
---
## Enable Selectively
### 1. Wireguard Config
```
# /etc/wireguard/wg0.conf

# local settings for Endpoint A
[Interface]
PrivateKey = AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEE=
# omit the Address, DNS, MTU, Table, and Pre/PostUp/Down settings
# Address = 10.0.0.1/32
ListenPort = 51821

# remote settings for Host β
[Peer]
PublicKey = fE/wdxzl0klVp/IR8UcaoGUMjqaWi3jAd7KzHKFS6Ds=
Endpoint = 203.0.113.2:51822
AllowedIPs = 0.0.0.0/0
```
### Creating and configuring Namespace
```(bash)
# Create a new network namespace named pvt-net1
sudo ip netns add pvt-net1

# Enable the loopback interface inside pvt-net1
sudo ip -n pvt-net1 link set lo up

# Create an empty WireGuard interface wg0 in the namespace
sudo ip -n pvt-net1 link create wg0 type wireguard

# Apply your WireGuard configuration file to wg0
sudo ip netns exec pvt-net1 wg setconf wg0 /etc/wireguard/wg0.conf

# Assign the single-host IP 10.0.0.1/32 to wg0
sudo ip -n pvt-net1 address add 10.0.0.1/32 dev wg0

# Bring the wg0 interface up
sudo ip -n pvt-net1 link set wg0 up

# Route all traffic in the namespace through wg0
sudo ip -n pvt-net1 route add default dev wg0
```

### Disabling Custom Netns
```(bash)
ip netns pids pvt-net1 | sudo xargs -r kill
sudo ip netns del pvt-net1
```

**Note** I currently cannot get disabling wireguard specifically for an app to work, i'll add to this guide if I find a way
