---
slug: run-npm-without-root-access
title: Run NPM Without Root Access
description: Menjalankan NPM tanpa sudo / doas (tanpa root access) dengan mengatur direktori global packages
date: 2023-04-30
author: Rahul
tags: ["web", "npm", "nodejs", "linux"]
featured: false
editable: true
---

<hr />

## [Introduction](#introduction)

NPM menginstal paket secara lokal di dalam proyek Anda secara default. Anda juga dapat menginstal paket secara global (mis. npm install -g <package>) (berguna untuk aplikasi baris perintah). Namun sisi negatifnya adalah Anda harus menjadi root (atau menggunakan sudo) untuk dapat menginstal secara global.

Berikut adalah cara untuk menginstal paket secara global untuk pengguna tertentu tanpa memerlukan akses root.

<figure>
  <img src="https://i.postimg.cc/gJ36Gyyg/Screenshot-from-2023-04-30-11-11-12.png" alt="NPM permission error" />
  <figcaption>Contoh NPM error saat instalasi package karena tidak diberi access root</figcaption>
</figure>

## [Setup Global Package Directory](#setup-global-package-directory)

### [Create Directory](#create-directory)

Buat direktori (folder) tempat _global package_:

```bash
mkdir "${HOME}/.npm-packages"
```

### [Configure NPM](#configure-npm)

Setting NPM ke direktori _global package_:

```bash
npm config set prefix "${HOME}/.npm-packages"
```

## [Environment Configuration](#environment-configuration)

### [Update Shell Configuration](#update-shell-configuration)

Tambahkan konfigurasi pada `~/.bashrc` atau `~/.zshrc`:

```bash
NPM_PACKAGES="${HOME}/.npm-packages"

export PATH="$PATH:$NPM_PACKAGES/bin"

# Preserve MANPATH if you already defined it somewhere in your config.
# Otherwise, fall back to `manpath` so we can inherit from `/etc/manpath`.
export MANPATH="${MANPATH-$(manpath)}:$NPM_PACKAGES/share/man"
```

### [Load New Configuration](#load-new-configuration)

_Load path_ yang sudah di tambahkan:

```bash
source ~/.bashrc
```

## [Verification](#verification)

Setelah konfigurasi selesai, Anda dapat menginstal package global tanpa sudo:

```bash
npm install -g package-name
```

Package yang terinstal akan tersimpan di direktori `~/.npm-packages` dan dapat diakses melalui PATH yang sudah dikonfigurasi.
