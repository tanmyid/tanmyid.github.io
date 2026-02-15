---
slug: fix-whatsapp-need-official
title: Fix WhatsApp Need Official
description: Tutorial lengkap untuk mengatasi masalah WhatsApp yang meminta aplikasi official pada perangkat Android yang sudah di-root
date: 2024-05-15
author: Tanio
tags: ["tutorial", "android", "root", "whatsapp"]
featured: true
editable: true
---

<hr />

## [Introduction](#introduction)

Bagi pengguna _advance_ Android, _rooting_ merupakan sebuah kebutuhan yang bisa dibilang wajib, karena dengan akses _root_ banyak manfaat yang didapat. Tentunya manfaat tersebut didapatkan ketika kita sudah paham apa yang dilakukan.

<br />

Akhir-akhir ini, raksasa Google melakukan _operasi masal_ pada perangkat yang terdeteksi _root_ sehingga Play Integrity nya _failed_. Hal ini berdampak juga bagi pengguna WhatsApp yang terdeteksi menggunakan aplikasi _unofficial_ padahal telah menggunakan aplikasi Official yang diunduh dari PlayStore.

<br />

## [Why This Happens](#why-this-happens)

Mungkin, bagi pihak Meta sebagai pengembang WhatsApp merasa perlu melakukan ini demi keamanan aplikasinya, mengingat ketika _user_ sudah mendapatkan hak akses _root_, banyak hal yang bisa dilakukan, termasuk memodifikasi aplikasi WhatsApp tersebut.

<br />

## [Requirements](#requirements)

Alat dan bahan yang dibutuhkan:

- **Rooted Device** dengan salah satu dari berikut:
  - [Magisk](https://github.com/topjohnwu/Magisk)
  - [KernelSU](https://github.com/tiann/KernelSU)
  - [Apatch](https://github.com/bmax121/APatch)
- [PlayIntegrityFix](https://github.com/chiteroman/PlayIntegrityFix/releases)
- [Playcurl](https://github.com/daboynb/PlayIntegrityNEXT/releases)
- [ZygiskNext](https://github.com/Dr-TSNG/ZygiskNext/releases) _(untuk enable Zygisk jika menggunakan KernelSU/Apatch)_
- [LSPosed](https://github.com/LSPosed/LSPosed/releases/download/v1.9.2/LSPosed-v1.9.2-7024-zygisk-release.zip)
- [LSPosed Mod](https://github.com/mywalkb/LSPosed_mod/releases) _(jika OS tidak mendukung Zygote32)_
- [Bootloader Spoofer](https://github.com/chiteroman/BootloaderSpoofer/releases)

<br />

## [Tutorial Steps](#tutorial-steps)

### [Step 1: Preparation](#step-1-preparation)

Download semua alat dan bahan yang sudah tertera di atas, sesuaikan dengan Root Manager yang Anda gunakan (Magisk / KernelSU / Apatch).

<br />

### [Step 2: Enable Zygisk](#step-2-enable-zygisk)

- **Magisk**: Pergi ke setting lalu `Enable Zygisk`
- **KernelSU dan Apatch**: Flash module ZygiskNext

<br />

### [Step 3: Install Modules](#step-3-install-modules)

1. Flash module **LSPosed** (jika perangkat tidak mendukung Zygote 32bit, flash LSPosed Mod)
2. Flash module **PlayIntegrityFix**
3. Flash module **Playcurl**:
   - Pertama tekan `Volume Down` (Install the fp downloader app)
   - Lalu `Volume Up` (FP auto, the app will run the fp)
   - Hal ini agar otomatis memperbarui file _pif.json_
4. Install **Bootloader Spoofer**
5. **Reboot Device**

<br />

### [Step 4: Configure LSPosed](#step-4-configure-lsposed)

- Buka LSPosed dengan lihat notifikasi sistem yang ada di QS Panel (Swipe Down StatusBar)
- Pilih tab module
- Aktifkan **Bootloader Spoofer**
- Checklist **WhatsApp** / **WhatsApp Business**
- **JANGAN** checklist kerangka sistem / system framework
- **Reboot Device**

<br />

### [Step 5: Clear Data](#step-5-clear-data)

- Masuk ke **Pengaturan** > **Aplikasi**
- Hapus Data **Google Play Store** dan **Google Play Service** (Layanan Google Play)
- **Reboot Device**

<br />

### [Step 6: Final Steps](#step-6-final-steps)

- Reinstall **WhatsApp** / **WhatsApp Business** dari Google Play Store
- Relogin dengan nomor Anda
- Semoga berhasil!

<br />

## [Why "Semoga Berhasil"?](#why-semoga-berhasil)

Ada beberapa yang sudah mencoba tutorial tersebut, akan tetapi tidak berhasil, karena memang nomor _handphone_ nya sudah di-banned permanent. Tapi tidak ada salahnya mencoba kan?

<br />

Ribet? Memang, namanya juga opreker Android! 😄

<br />

## [Note](#note)

Mohon maaf karena tutorial kali ini tidak menggunakan gambar/screenshot, karena penulis sendiri tidak mengalami hal tersebut. Tutorial ini berdasarkan pengalaman penulis saat melakukan diskusi di grup Telegram.

<br />

## [References](#references)

- [Redmi Note 7 | Lavender Indonesia](https://t.me/RedmiNote7Indonesia)
- [MdgWa Module](https://t.me/mdgwamodule)
