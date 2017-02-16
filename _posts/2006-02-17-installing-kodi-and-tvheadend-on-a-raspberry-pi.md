---
layout: post
title: Installing Kodi and TVHeadEnd on a Raspberry Pi
categories:
- raspberrypi
tags: [tvheadend, raspberrypi, kodi]
status: publish
type: post
published: false
meta: {}
author: Luke Smith
---

Recently I ditched Sky, after 10 years and alot of £££, and moved to a legal [Kodi](https://kodi.tv) setup.

Considering I already had a satellite dish and cables, going with [FreeSat](http://www.freesat.co.uk/) made perfect sense. I just needed a new box to plug them into. I could have purchased an off the shelf FreeSat box, but where's the fun in that? The hunt was on to see how I could build my own setup.

## Equipment

- [Raspberry Pi 3](http://amzn.to/2lSwDz2) - I started with one, but I am now moving to having two for my setup.
- A DVB-S2 Tuner - I found the [Hauppauge PCTV DVB-S2 Stick 461e](http://amzn.to/2lSrk2s) works perfectly. You need 1 for each LNB.

## Installation

### Selecting the Operating System

First you need to install an Operating System on your Raspberry Pi SD card for running Kodi. Whether you're using one or two pi's then go for either [OSMC](https://osmc.tv/) or [Libreelec](http://libreelec.tv/). These are OS that come with Kodi and are built for running as a media center.

Second you need something to run the tuner software on. You can either install it on the same device as Kodi above, or use a second Raspberry Pi for this. As I want to remove as many cables from my living room as possible I've gone for a second pi, that I can hide away in the garage, running [Raspbian Jessie Lite](https://www.raspberrypi.org/downloads/raspbian/).

In both cases, follow the [installing images](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) documentation on the Raspberry Pi website.

Note: Raspbian Pixel was [updated to disable SSH access](https://www.raspberrypi.org/blog/page/6/?fish#a-security-update-for-raspbian-pixel) by default. If you aren't planning on connecting a keyboard+mouse upto the devices you'll want to add a file named `ssh` to the SD card after writing the OS to them, so SSH will be enabled.
