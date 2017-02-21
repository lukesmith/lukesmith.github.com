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

### Selecting the Operating System(s)

First you need to install an Operating System on your Raspberry Pi SD card for running Kodi. Whether you're using one or two pi's then go for either [OSMC](https://osmc.tv/) or [Libreelec](http://libreelec.tv/). These come with Kodi and are built for running as a media center.

Second you need something to run the tuner software on. You can either install it on the same device as Kodi above, or use a second Raspberry Pi for this. As I want to remove as many cables from my living room as possible I've gone for a second pi, that I can hide away in the garage, running [Raspbian Jessie Lite](https://www.raspberrypi.org/downloads/raspbian/).

In both cases, follow the [installing images](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) documentation on the Raspberry Pi website.

Note: Raspbian Pixel was [updated to disable SSH access](https://www.raspberrypi.org/blog/page/6/?fish#a-security-update-for-raspbian-pixel) by default. If you aren't planning on connecting a keyboard+mouse upto the devices you'll want to add a file named `ssh` to the SD card after writing the OS to them, so SSH will be enabled. Remember to change the default password for the `pi` the first time you connect. 

### Installing TVHeadend

TVHeadend is what connects to the tuners, and produces a stream that can then be accessed by Kodi.

If you're using Raspbian Jessie then you use the following based on the [TVHeadend instructions](https://tvheadend.org/projects/tvheadend/wiki/AptRepository).

Connect to your PI and open up a terminal and run the following.

```shell
sudo apt update
sudo apt install apt-transport-https
```

You need to do the above before installing tvheadend, because bintray uses `https` and you first need to install the `apt-transport-https` package.

```shell
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 379CE192D401AB61
echo "deb https://dl.bintray.com/tvheadend/deb jessie stable" | sudo tee -a /etc/apt/sources.list
sudo apt-get update
sudo apt-get install tvheadend
```

You should now be able to connect to your TVHeadend server from remotely via http://{pi_ip}:9981.

At this time TVHeadend is running but needs to be configured. If using the [Hauppauge PCTV DVB-S2 Stick 461e](http://amzn.to/2lSrk2s) then the drivers need to be installed. Open up a terminal, or SSH, to the TVHeadend Pi and run

```shell
wget https://github.com/OpenELEC/dvb-firmware/blob/master/firmware/dvb-demod-m88ds3103.fw?raw=true
sudo mv dvb-demod-m88ds3103.fw\?raw\=true /lib/firmware/dvb-demod-m88ds3103.fw
```

You may need to reboot the Pi

```shell
sudo reboot
```

Once rebooted you can add your USB Tuner and and use the TVHeadend web ui to configure things. Note: Although the Rasperry Pi can power the USB Tuner, I recommend using an external power-source for them. Without using external power (or when trying to run multiple tuners) I found the Pi would randomly freeze and require the 'power-it-off' and 'back-on' fix.

### Configuring the Kodi server

To keep down the cost of the Raspberry Pi, it doesn't ship with the required codecs to play the video streams that TVHeadend makes available. These need to be purchased separately and the license keys installed onto the pi. This only needs to be done for the Pi running Kodi. How To Geek has full instructions on [how to add mpeg 2 and vc1 video codecs](https://www.howtogeek.com/137654/how-to-add-mpeg-2-and-vc-1-video-codec-support-to-your-raspberry-pi/) to a pi.

You will then need to install the [Kodi PVR TVHeadend Client](http://kodi.wiki/view/Tvheadend#Connecting_Kodi_to_Tvheadend) and configure it to point at your TVHeadend server.
