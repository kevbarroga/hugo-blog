---
title: "Install Telegram Messaging App for Desktop"
date: 2017-08-09
tags: ["telegram", "linux", "ubuntu"]
draft: false
---

## Step 1. Download Telegram

Goto [Telegram Desktop](https://desktop.telegram.org/) and download the appropriate
version for your operating system.

Save it to somewhere specific ex. `~/Downloads` as we will be moving into the directory in the next step.

## Step 2. Extract files

Move into the directory in which you saved the file. As in our case `cd ~/Downloads`.

Extract the *tar* file:

`tar -xJvf tsetup.X.X.X.tar.xz`

## Step 3. Move Telegram to suitable location

Move the extracted *Telegram* folder to */opt/telegram* directory:

`sudo mv Telegram /opt/telegram`

Create soft link of *Telegram* to */usr/bin/telegram*:

`sudo ln -sf /opt/telegram/Telegram /usr/bin/telegram`

## Step 4. Launch Telegram

While in the terminal you can start Telegram with this command:

`./Telegram`

The program will launch and ask you to enter your phone number.

## Step 5. Use Telegram

You may now start messaging your friends and annoy them with cute telegram stickers!
