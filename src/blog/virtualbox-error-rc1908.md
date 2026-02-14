---
slug: virtualbox-error-rc1908
title: VirtualBox Kernel Driver Not Installed (rc=-1908)
description: Mengatasi error VirtualBox Kernel driver not installed (rc=-1908) pada Linux
date: 2019-09-04
author: Rahul
tags: ["linux", "virtualbox", "troubleshooting"]
featured: true
editable: true
---

<hr />

## [Introduction](#introduction)

Kebetulan inget dan di ingetin lewat post yang ada di _IndoXploit_ tentang **Kernel driver not installed (rc=-1908)** yang dimana kita tidak dapat menjalankan mesin virtual yang telah kita buat seperti pada gambar di bawah ini.

<figure>
  <img src="https://i.postimg.cc/59w4F6Wq/image.png" alt="VirtualBox error rc=-1908" />
  <figcaption>Error VirtualBox Kernel driver not installed</figcaption>
</figure>

## [Penyebab Error](#penyebab-error)

Dan kalian jika baru saja menginstall virtualbox pada Archlinux (Di sini saya menyebut archlinux karena saya yang kerap mengalami dan menemui masalah tersebut) akan mendapatkan error seperti berikut:

```bash
~ ❯ sudo pacman -S virtualbox
[sudo] password for tan:
resolving dependencies...
:: There are 2 providers available for VIRTUALBOX-HOST-MODULES:
:: Repository community
   1) virtualbox-host-dkms  2) virtualbox-host-modules-arch

Enter a number (default=1):
looking for conflicting packages...

Packages (4) dkms-2.7.1-1  sdl-1.2.15-10  virtualbox-host-dkms-6.0.10-1  virtualbox-6.0.1

Total Download Size:    42.11 MiB
Total Installed Size:  162.24 MiB

:: Proceed with installation? [Y/n]
:: Retrieving packages...
 sdl-1.2.15-10-x86_64                                                       341.3 KiB  81
 dkms-2.7.1-1-any                                                            51.4 KiB  3.
 virtualbox-host-dkms-6...   682.3 KiB   797K/s 00:01 [----------------------------] 100%
 virtualbox-6.0.10-1-x86_64   41.1 MiB   806K/s 00:52 [----------------------------] 100%
(4/4) checking keys in keyring                        [----------------------------] 100%
(4/4) checking package integrity                      [----------------------------] 100%
(4/4) loading package files                           [----------------------------] 100%
(4/4) checking for file conflicts                     [----------------------------] 100%
(4/4) checking available disk space                   [----------------------------] 100%
:: Processing package changes...
(1/4) installing sdl                                  [----------------------------] 100%
Optional dependencies for sdl
    alsa-lib: ALSA audio driver [installed]
    libpulse: PulseAudio audio driver [installed]
(2/4) installing dkms                                 [----------------------------] 100%
Optional dependencies for dkms
    linux-headers: build modules against the Arch kernel
    linux-lts-headers: build modules against the LTS kernel
    linux-zen-headers: build modules against the ZEN kernel
    linux-hardened-headers: build modules against the HARDENED kernel
(3/4) installing virtualbox-host-dkms                 [----------------------------] 100%
Optional dependencies for virtualbox-host-dkms
    linux-headers: build modules against Arch kernel
    linux-lts-headers: build modules against LTS kernel
    linux-zen-headers: build modules against ZEN kernel
(4/4) installing virtualbox                           [----------------------------] 100%
Optional dependencies for virtualbox
    vde2: Virtual Distributed Ethernet support
    virtualbox-guest-iso: Guest Additions CD image
    virtualbox-ext-vnc: VNC server support
    virtualbox-sdk: Developer kit
:: Running post-transaction hooks...
(1/8) Creating system user accounts...
(2/8) Install DKMS modules
==> Unable to install module vboxhost/6.0.10_OSE for kernel *: Missing kernel headers.
(3/8) Updating icon theme caches...
(4/8) Reloading system manager configuration...
(5/8) Reloading device manager configuration...
(6/8) Arming ConditionNeedsUpdate...
(7/8) Updating the desktop file MIME type cache...
(8/8) Updating the MIME type database...
```

Bagian ini `==> Unable to install module vboxhost/6.0.10_OSE for kernel : Missing kernel headers.` adalah penyebab virtualbox tidak bisa jalan.

## [Solusi](#solusi)

### [Install Kernel Headers](#install-kernel-headers)

Untuk mengatasinya lakukan instalasi kernel headers :

```bash
sudo pacman -S linux-headers
```

### [Untuk Kernel LTS](#untuk-kernel-lts)

Untuk yang menggunakan kernel LTS:

```bash
sudo pacman -S linux-lts-headers
```

### [Detail Instalasi](#detail-instalasi)

Berikut rinciannya :

```bash
~ ❯ sudo pacman -S linux-headers                                                  1m 41s
resolving dependencies...
looking for conflicting packages...

Packages (1) linux-headers-5.2.11.arch1-1

Total Download Size:    17.70 MiB
Total Installed Size:  100.32 MiB

:: Proceed with installation? [Y/n]
:: Retrieving packages...
 linux-headers-5.2.11.a...    17.7 MiB   676K/s 00:27 [----------------------------] 100%
(1/1) checking keys in keyring                        [----------------------------] 100%
(1/1) checking package integrity                      [----------------------------] 100%
(1/1) loading package files                           [----------------------------] 100%
(1/1) checking for file conflicts                     [----------------------------] 100%
```

## [Verification](#verification)

Setelah instalasi kernel headers selesai, coba jalankan kembali VirtualBox. Error `rc=-1908` seharusnya sudah teratasi dan Anda dapat menjalankan virtual machine dengan normal.
