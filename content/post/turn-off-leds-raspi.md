---
title: "Turn Off Raspberry Pi Leds"
date: 2017-08-18
tags: ["raspberrypi", "pi", "led", "development"]
draft: false
---

## Step 1. Change to root user

In your terminal change to *root* user:

`sudo su`

## Step 2. Turn of red/green led

To turn off the red led:

`echo 0 > /sys/class/leds/led0/brightness`

To turn off the green led:

`echo 0 > /sys/class/leds/led1/brightness`

## Step 3. Stealth mode

Your raspberry pi is now in incognito!!

_*Leds will turn back on after reboot_

