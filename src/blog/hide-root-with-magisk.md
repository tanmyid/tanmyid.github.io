---
slug: hide-root-with-magisk
title: Hide Root With Magisk
description: Berbagai metode untuk menyembunyikan root Android dengan Magisk agar aplikasi perbankan tetap bisa digunakan
date: 2023-04-27
author: Rahul
tags: ["magisk", "android", "root", "banking", "tutorial"]
featured: false
editable: true
---

<hr />

## [Introduction](#introduction)

Bagi para opreker Android, pasti sudah tidak asing lagi dengan yang namanya Magisk. Ya, Magisk adalah aplikasi Android yang dikembangkan oleh John Wu yang dapat digunakan untuk mengizinkan dan menyembunyikan penggunaan root dan dapat memastikan bahwa lolos SafetyNet.

<br />

Bisa dibilang Magisk ini adalah pengganti SuperSU yang untuk jaman sekarang sudah _usang_.

<br />

## [Problem](#problem)

Pada awal-awal rilis, Magisk ini sangat keren karena memiliki fitur _Hide Root_ agar aplikasi yang kita pilih tidak bisa mendeteksi bahwa HP kita terpasang Magisk. Kebanyakan aplikasi yang ada sangkut pautnya dengan keuangan seperti M-Banking, E-Wallet atau E-Money tidak mengizinkan aplikasinya dibuka pada perangkat yang sudah dimodifikasi (dalam tanda kutip sudah di-"root").

<br />

Nah, tapi developer M-Banking, E-Wallet atau E-Money tidak kalah akal. Setelah fitur _Hide Root_ ini booming, maka para developer meng-update security aplikasinya agar tetap bisa mendeteksi Magisk walau sudah di-_hide root_.

<br />

## [Solutions](#solutions)

Ada 3 cara yang saya bahas di sini, bagaimana mengakali _Hide Root_ bawaan Magisk yang sudah tidak bisa yaitu:

1. **Metode Zygisk + Shamiko**
2. **Metode Magisk Mod** - di sini saya membahas Magisk Delta
3. **Metode Magisk Freeze App**

_(Untuk metode ke-3 ini, mirip metode pertama tetapi ada penambahan module)_

<br />

## [Metode Zygisk + Shamiko](#metode-zygisk-shamiko)

Salah satu metode yang paling sering digunakan karena terhitung simple.

**Steps:**

- Download Magisk di [GitHub](https://github.com/topjohnwu/Magisk/releases), saya sarankan pakai versi minimal 25.2
- Download dan flash module [Shamiko](https://t.me/magiskalpha/550?single)
- Hide the Magisk App, kasih nama random lalu install

<figure>
  <img src="https://telegra.ph/file/15dbecad3b28c2f787db4.jpg" alt="Hide Magisk App" />
  <figcaption>Hide App</figcaption>
</figure>

- Aktifkan mode Zygisk tapi **jangan centang Enforce DenyList**

<figure>
  <img src="https://telegra.ph/file/0246d657d5495a99c510b.jpg" alt="Activate Zygisk" />
  <figcaption>Zygisk Settings</figcaption>
</figure>

- Configure DenyList untuk nge-hide root aplikasi yang diinginkan

<figure>
  <img src="https://telegra.ph/file/daaa8f26d42a649f827d8.jpg" alt="Configure DenyList" />
  <figcaption>Configure DenyList</figcaption>
</figure>

<br />

## [Metode Magisk Mod](#metode-magisk-mod)

Magisk 25.2 (Zygisk) + Shamiko sekarang sudah terdeteksi sama beberapa aplikasi mobile banking. Kebetulan kemarin pagi nemu chat di grup Telegram bahas soal Magisk Delta.

<br />

Setelah saya coba uninstall Magisk 25.2 (Zygisk) terus pasang Magisk Delta ada beberapa Mobile Banking yang terkenal alot buat bypass rootnya bisa tembus.

<br />

### [List Mobile Banking yang Tembus](#list-mobile-banking-yang-tembus)

- Line Bank v 2.2.25 (latest PlayStore)
- Octo Mobile v 2.8.7 (latest PlayStore)
- BRImo v 2.35.0 (latest PlayStore)
- BCA Mobile v 4.0.2 (latest PlayStore)
- Blu BCA v 1.30.0 (latest PlayStore)
- BNI Mobile Banking v 5.9.1

<br />

### [List yang Crash](#list-yang-crash)

- Livin' by Mandiri v1.2.0 (latest PlayStore)

<br />

### [Tutorial Install Magisk Delta](#tutorial-install-magisk-delta)

- Uninstall Magisk 25.2
- Download Magisk Delta di [HuskyDG](https://huskydg.github.io/magisk-files/) - Download yang Debug
- Rename ke .zip kalau TWRP atau OFox nya belum support flash Magisk versi .apk
- Flash Magisk Delta via TWRP
- Masuk ke Setting > Konfigurasi MagiskHide, nah centang Mobile Banking yang kamu punya
- Buka Mobile Banking tersebut

<br />

**Kelemahan metode ini:**

- Tidak pakai Zygisk, jadi module-module yang butuh Zygisk tidak bisa jalan. Kalau Zygisk diaktifkan, mobile banking bakal ngedetect root.

<br />

## [Metode Magisk App Freeze](#metode-magisk-app-freeze)

Metode ini sama seperti metode pertama, cuma nambah Module Magisk App Freeze:

- Hide Magisk App dan Centang Zygisk (tutorial sama seperti di atas)
- Download [Magisk App Freezer](https://github.com/tanmyid/lavender-files/raw/main/magiskapp_freezer_v1.4.zip)
- Flash Module
- Done

<br />

### [Cara Kerja](#cara-kerja)

Magisk akan nge-freeze (hilang dari peradaban) kalau kita buka aplikasi yang ada di DenyList. Nah biar Magisk nya muncul lagi, force close aplikasi DenyList yang berjalan.

<figure>
  <img src="https://i.postimg.cc/mgzcQhRP/u07-Wgx-Bti6r-N.png" alt="Magisk App Freeze Description" />
  <figcaption>Deskripsi Magisk App Freeze</figcaption>
</figure>

<br />

## [Conclusion](#conclusion)

Berbagai metode di atas bisa dicoba sesuai dengan kebutuhan dan kompatibilitas perangkat. Setiap metode memiliki kelebihan dan kekurangan masing-masing.

<br />

### [References](#references)

- [Hide Root - Metode Shamiko](https://telegra.ph/Hide-Root---Metode-Shamiko-hide-zygisk-01-31)
- [Facebook Post](https://www.facebook.com/sindikat.krikil/posts/pfbid0ku3u8MpYJD8Mt7uKz56pakNd2L8LB4Fq2y6qvkRWyi1suC3MCKDQtyeGX39KUCz2l)
