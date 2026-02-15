---
slug: xss-files-dot-fm
title: Cross Site Scripting Files Dot Fm
description: Cross Site Scripting di website Files.fm melalui filename upload vulnerability
date: 2019-08-31
author: Tanio
tags: ["pentest", "xss", "security", "file-upload"]
featured: false
editable: true
---

<hr />

## [Introduction](#introduction)

Hallo lur, kembali dengan Write Up _XSS on file upload_. Maksudnya gimana lur? Jadi gini lur, XSS yang akan saya tulis kali ini adalah XSS file upload dimana kita menyisipkan script XSS nya pada nama file gambar tersebut.

Nah target kali ini adalah Files.Fm sekali lagi tidak ada reward kali ini dan saya sudah meminta izin adminnya untuk melakukan Write Up. Untuk mengetahui apa itu Files.fm bisa mengunjungi Link Berikut.

## [Important Note](#important-note)

```
"Trik ini hanya berlaku untuk sistem operasi linux, di karenakan windows tidak mengijinkan kita merename dengan karakter **< >**. Hindari juga pemakaian **/** sudah pasti tidak di ijinkan"
```

## [Step by Step](#step-by-step)

### [Prepare the File](#prepare-the-file)

Oke langsung saja, pertama siapkan sebuah gambar apa aja terserah, mau gambar monyet, foto mantan juga boleh hehe. Lalu rename dengan script XSS, misal seperti berikut :

```php
<h2 onmouseover="alert('XSS')">.png
```

<figure>
  <img src="https://i.postimg.cc/DyKbtn8w/filename.png" alt="Renamed file with XSS payload" />
  <figcaption>File yang sudah direname dengan payload XSS</figcaption>
</figure>

### [Upload the File](#upload-the-file)

Lalu upload file yang sudah di rename tadi

<figure>
  <img src="https://i.postimg.cc/2jn1dM2R/files-fm.png" alt="Upload process" />
  <figcaption>Proses upload file</figcaption>
</figure>

### [Trigger the XSS](#trigger-the-xss)

Setelah di upload, coba sorot bagian image uploadnya dan duarrrr nmex

<figure>
  <img src="https://i.postimg.cc/DydbhHXd/got-XSS.png" alt="XSS triggered" />
  <figcaption>XSS berhasil terpicu</figcaption>
</figure>

## [Explanation](#explanation)

Intinya adalah, kita cuma menambahkan script XSS pada _filename_ nya saja, simple bukan?

## [Kesimpulan](#kesimpulan)

Sekian tulisan kali ini, jika ada kesalahan mohon di maafkan. Terima Kasih
