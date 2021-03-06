---
title: "Install KeePassXC"
date: 2017-11-12
tags: ["keepassxc", "linux", "ubuntu"]
draft: false
---

## Introduction

Creating long secure passwords can be difficult. Trying to find a way to store them securely is another story.
That is why I always recommend to friends and family to start using a password manager.
A good password manager let you store your passwords in a secure database,
associate a key file with you database for even tighter security,
generate long random passwords for new accounts, and auto-type username and passwords for you.
You will only need to remember a single password that opens your password database.
Today we will be installing the [KeePassXC password manager](https://keepassxc.org).
KeePassXC is a fork of [KeePassX](https://www.keepassx.org/), which hasn't seen much development recently,
and is a cross platform port of [KeePass Password Safe](http://keepass.info/).



## Step 1. Download KeePassXC AppImage

Go to [KeePassXC](https://keepassxc.org/download#linux) and download the Official AppImage.

## Step 2. Make the AppImage executable

Move into the directory in which you saved the file, as in our case `cd ~/Downloads`.

Make the AppImage executalbe:

`chmod a+x KeePassXC-x.x.x-x86_64.AppImage`

## Step 3. (Optional) Move KeePassXC to a suitable location

Move the KeePassXC AppImage *KeePassXC-x.x.x-x86_64.AppImage* to */opt/keepassxc* directory:

`mv KeePassXC-x.x.x-x86_64.AppImage /opt/keepassxc/`

## Step 4. Executing AppImage

You can execute the AppImage as follows:

`./KeePassXC-x.x.x-x86_64.AppImage`

## Step 5. (Optional) Add .desktop file

There's an issue with keeping the KeePassXC app icon(not sure if OS or AppImage) dockable in elementary OS.

I created a *.desktop* file `.local/share/applications/appimagekit-keepassxc.desktop` with the contents below:

```
[Desktop Entry]
Name=KeePassXC
GenericName=Community Password Manager
GenericName[de]=Passwortverwaltung
GenericName[es]=Gestor de contraseñas
GenericName[fr]=Gestionnaire de mot de passe
GenericName[ru]=менеджер паролей
Exec="/opt/keepassxc/KeePassXC-x.x.x-x86_64.AppImage" %U
Icon=appimagekit-keepassxc
Terminal=false
Type=Application
Categories=Qt;Utility;
MimeType=application/x-keepass2;
X-Desktop-File-Install-Version=0.22
X-AppImage-Comment=Generated by /tmp/.mount_KeePasBjphW0/usr/bin//keepassxc_env.wrapper
TryExec=/opt/keepassxc/KeePassXC-x.x.x-x86_64.AppImage

Actions=Uninstall;

[Uninstall]
Name=Remove desktop integration for KeePassXC
Exec="/opt/keepassxc/KeePassXC-x.x.x-x86_64.AppImage" --remove-appimage-desktop-integration
```

After a restart, KeePassXC can be kept in dock in elementary OS's application launcher.

## Step 6. Use KeePassXC

You may now store various account passwords in a secure and open source password manager!