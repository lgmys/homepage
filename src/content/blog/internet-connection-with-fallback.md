---
title: 'Adding fallback internet connection to my home network'
description: 'How I dealt with occassional internet connection failures at my home'
pubDate: 'Jan 13th 2026'
heroImage: '../../assets/blog-placeholder-3.jpg'
---

Every now and then, I experience internet connection fallbacks—sometimes spectacular ones. For example, during a roof renovation, the aerial fiber cable was moved by the renovation team to a height below what is required by Polish law and was subsequently snapped by a garbage truck.

Other times, it’s just an unreliable ISP. They do maintenance or something similar, which results in annoyed family members and me being unable to work from home.

Since I’m a heavy Home Assistant user and a DIY enthusiast with some experience with the ESP32, I decided to solve this somehow.

The idea was as follows:

The ISP’s fiber router/modem exposes its own Wi-Fi network

I run my own mesh network using the ISP router as a gateway

I have an LTE router with a LAN port (bought on sale) and a switch

I use Home Assistant with smart plugs to conditionally toggle between the fiber and LTE routers

To make this work, I needed a device that could probe the fiber router for internet connectivity.

Skipping the ugly code, I made the device alternate between my home network and the fiber router’s Wi-Fi network. When connected to the fiber router’s Wi-Fi, it attempts a TCP connection to Cloudflare’s DNS server. The result is then broadcast to Home Assistant via MQTT once the device reconnects to my home network. This cycle repeats every minute.

If the fiber router does not have an internet connection, Home Assistant disables the switch that sits between the ISP router and the main network and enables the LTE router instead. Note that the ISP fiber router is never disabled, so we can continue monitoring it and detect when the internet connection is restored.

That’s about it! I hope this inspired you in some way.
