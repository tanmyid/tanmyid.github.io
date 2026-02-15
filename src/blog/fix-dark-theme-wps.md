---
slug: fix-dark-theme-wps
title: Fix Dark Theme WPS Office Linux
description: Solusi untuk mengatasi masalah dark theme GTK di WPS Office yang menggunakan Qt framework
date: 2021-02-09
author: Tanio
tags: ["tutorial", "linux", "wps", "office", "theme"]
featured: false
editable: true
---

<hr />

## [Introduction](#introduction)

Dari pengguna Windows yang hijrah ke Linux, pasti mencari alternatif Microsoft Office, tetapi terkendala masalah format dokumen yang acak-acakan atau font yang tidak muncul.

<br />

Maka dari itu ada alternatif yaitu WPS Office. Selama pemakaian untuk kepentingan kuliah, WPS Office sangat membantu karena interface yang mirip dengan Microsoft Office dan merupakan salah satu program office yang sangat user friendly.

<br />

## [WPS Office Components](#wps-office-components)

WPS Office menyediakan komponen yang cukup lengkap:

- **WPS Writer** - Word processor
- **WPS Presentation** - Presentation software
- **WPS Spreadsheet** - Spreadsheet application
- **WPS PDF** - PDF reader and editor

<br />

## [Problem](#problem)

Tetapi ada masalah yang cukup serius, yaitu masalah jika kita mengaktifkan dark theme GTK, karena secara default, WPS Office menggunakan Qt framework.

<figure>
  <img src="https://i.postimg.cc/J4VC7NNp/2019-08-23-013446-1366x768-scrot.png" alt="WPS Office dark theme problem" />
  <figcaption>Problem: Teks tidak terlihat karena konflik theme</figcaption>
</figure>

Seperti gambar di atas, kita tidak bisa lihat karakter, karena WPS secara default membaca tema Qt bukan GTK.

<br />

## [Files to Edit](#files-to-edit)

Sebelum ke cara fixnya, perlu diketahui file mana saja yang akan diedit:

```
/usr/bin/wps     (WPS Writer)
/usr/bin/wpp     (WPS Presentation)
/usr/bin/et      (WPS Spreadsheet)
/usr/bin/wpspdf  (WPS PDF)
```

<br />

## [Solution](#solution)

Di sini saya menggunakan _nano_ untuk editing. Anda bisa menggunakan text editor favorit Anda:

```shell
sudo nano /usr/bin/wps
```

Ganti baris `gOpt=` dengan script di bawah:

```bash
gOpt="-style=gtk+"
export GTK2_RC_FILES=/usr/share/themes/Matcha-azul/gtk-2.0/gtkrc
```

Untuk _Matcha-azul_ bisa kalian ganti dengan _light theme_ yang akan dipakai. **Penting: pakai light theme ya, jangan dark theme**.

<br />

Lakukan hal yang sama untuk semua aplikasi WPS di atas:

- `/usr/bin/wps` (WPS Writer)
- `/usr/bin/wpp` (WPS Presentation)
- `/usr/bin/et` (WPS Spreadsheet)
- `/usr/bin/wpspdf` (WPS PDF)

<br />

## [Result](#result)

Setelah melakukan perubahan di atas, WPS Office akan menggunakan GTK theme dan dapat berjalan normal dengan dark theme system tanpa masalah visibility pada teks.

<br />

**Note**: Pastikan theme yang dipilih kompatibel dan tidak menyebabkan masalah rendering pada aplikasi.
