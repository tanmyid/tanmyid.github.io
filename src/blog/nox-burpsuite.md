---
slug: nox-burpsuite
title: Nox Burpsuite
description: Tutorial setting up Burp Suite dengan Nox Android emulator untuk testing mobile applications
date: 2023-03-16
author: Rahul
tags: ["android", "burpsuite", "emulator", "pentest"]
featured: false
editable: true
---

<hr />

## [Introduction](#introduction)

Tutorial konfigurasi Nox player dengan Burp Suite untuk melakukan penetration testing pada aplikasi Android. Setup ini berguna untuk intercepting traffic dari aplikasi mobile dalam environment yang terkontrol.

## [Setup Requirements](#setup-requirements)

Sebelum memulai, pastikan Anda sudah memiliki:
- Nox Player (Android emulator)
- Burp Suite (Community atau Professional)
- Koneksi internet yang stabil

## [Configuration Steps](#configuration-steps)

### [Setting up Nox Player](#setting-up-nox-player)

Konfigurasi dasar Nox player untuk proxy settings.

### [Burp Suite Proxy Configuration](#burp-suite-proxy-configuration)

Setup proxy listener pada Burp Suite untuk menerima traffic dari emulator.

### [Certificate Installation](#certificate-installation)

Install CA certificate Burp Suite ke dalam Android emulator.

### [Testing the Setup](#testing-the-setup)

Verifikasi bahwa traffic dari aplikasi Android dapat ter-intercept dengan benar di Burp Suite.