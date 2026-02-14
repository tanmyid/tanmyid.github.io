---
slug: sbc-kerehore
title: Single Board Computer Bagi Kaum Kere Hore
description: Alternatif murah SBC menggunakan STB bekas Indihome untuk kaum yang budget terbatas
date: 2021-02-09
author: Rahul
tags: ["sbc", "stb", "hardware", "budget"]
featured: true
editable: true
---

<hr />

## [Introduction](#introduction)

Hai man teman, dah lama ndak ngeblog, kali ini gw akan sharing sedikit tentang apa yang gw temuin 2 bulan ini. Gw akan membahas tema sesuai judul yaitu **Single Board Computer Bagi Kaum Kere Hore**.

Oke sebelum ke pembahasan, gw jelasin sedikit tentang apa itu **SBC**.

## [Penjelasan SBC](#penjelasan-sbc)

**Single Board Computer** adalah komputer yang lengkap dibangun pada papan sirkuit tunggal, berikut mikroprosesor(s), memori, input / output (I/O) dan fitur lain yang dibutuhkan pada sebuah komputer fungsional.

Komputer single-board dibuat termasuk sebagai platform pengembangan sistem, untuk sistem pendidikan, atau untuk digunakan sebagai pengendali komputer tertanam (embedded). Banyak jenis komputer portabel yang mengintegrasikan semua fungsi mereka ke sebuah papan sirkuit tunggal. [sumber SBC](https://jogjaweb.co.id/blog/pengertian-dan-jenis-single-board-computer)

Masih bingung? oke gw jelasin secara sederhana, **SBC** dalam kata lain adalah **mini komputer**. Dimana sebuah motherboard yang biasanya berukuran segede buku tulis, bahkan ada yang segede buku gambar A4 di kecilin, sampe segede bungkus rokok. Gimana udah dapet gambarannya belum? harusnya si sudah hehe.

### [Jenis-jenis SBC](#jenis-jenis-sbc)

Nah sekarang ini banyak banget jenis jenis **SBC** yang tersebar di pasaran, antara lain :

- Raspberry Pi
- Odroid
- ASUS Tinker Board
- Libre Renegade Computer Board
- Arduino
- LattePanda
- Rock PI
- Banana Pi
- Orange Pi
- Khadas Vim

dan masih banyak lagi merk & jenis SBC yang beredar di pasaran.

### [Fungsi dan Harga](#fungsi-dan-harga)

Untuk fungsinya sendiri ada banyak, yang umum adalah di gunakan untuk micro controler dan server. Sekarang juga sudah banyak yang menggunakan SBC menjadi sebuah komputer desktop.

Untuk harga, bisa kalian dapatkan mulai Rp 500.000 - Rp 2.000.000 an. Gimana? kalau menurut temen temen harga segitu sudah murah, silahkan membeli hehe, tapi bagi diri saya sendiri nominal Rp 500.000 itu masih gede banget, apa lagi sekelas kuli yang kerjanya ikut orang lain :D

## [Alternatif Murah: STB Bekas Indihome](#alternatif-murah-stb-bekas-indihome)

Nah maka dari itu lah, gw sebagai kaum kere hore merasa terpanggil untuk menulis artikel ini. Yang akan kita bahas adalah alternatif yang lebih murah dari SBC yang sudah gw sebutin di atas, yaitu STB bekas Indihome.

STB (Set Top Box) Indihome selain berguna sebagai android TV, bisa juga di install sistem operasi GNU/Linux. STB Ex Indihome ini merupakan salah satu single board computer yang bisa menghandel mini server dan desktop.

Kalian bisa mendapatkannya di toko online dengan harga mulai Rp 200.000 - Rp 300.000. nah lumayan kan, ada sisa Rp 200.000 dari harga SBC di awal, terutama bagi anak kost, duit segitu bisa buat stock indomie + promag selama sebulan :D

### [Keunggulan STB Ex Indihome](#keunggulan-stb-ex-indihome)

Memang untuk ukuran, STB Ex Indihome ini lebih besar dari SBC yang udah gw sebutin di atas, tapi perbandingan ukurannya ga jauh jauh amat kok, malah STB Ex Indihome ini udah ada casing nya, jadi ndak usah beli casing lagi :D

Seri STB Ex Indihome yang (saya tahu) bisa di install linux adalah seri B860H & HG680P. Untuk seri yang lain, sepertinya belum bisa. Gw saranin pake yang ram 2gb, tenang ga selisih seberapa kok.

<figure>
  <img src="images/sbc-kere-hore.jpg" alt="STB B860H & HG680P" />
  <figcaption>STB B860H & HG680P</figcaption>
</figure>

### [Spesifikasi Hardware](#spesifikasi-hardware)

| **Hardware** | B860H v2.1                                | HG680P                                    |
| ------------ | ----------------------------------------- | ----------------------------------------- |
| SoC          | Amlogic S905X                             | Amlogic S905X                             |
| CPU          | Quad core ARM Cortex-A53 @ up to 1.54 GHz | Quad core ARM Cortex-A53 @ up to 1.54 GHz |
| GPU          | Mali-450MP                                | Mali-450MP                                |
| RAM          | 2GB                                       | 2GB                                       |
| STORAGE      | 8GB                                       | 8GB                                       |
| NETWORK      | Wifi build in & Ethernet                  | Wifi build in & Ethernet                  |
| DISPLAY      | HDMI                                      | HDMI                                      |
| USB 2.0      | 2x port                                   | 2x port                                   |
| USB 3.0      | NO                                        | NO                                        |
| PORT SDCARD  | Yes                                       | Yes                                       |
| PORT AUX     | Yes                                       | Yes                                       |

Soal spesifikasi, ndak ada perbedaan, cuma bungkus (casing) & susunan port yang berubah.

## [Sistem Operasi Yang Didukung](#sistem-operasi-yang-didukung)

Secara umum, tutorial yang bertebaran di internet, SBT tersebut biasa di install armbian OS GNU/Linux yang menggunakan apt sebagai paket manager.

Namun, ternyata tidak cuma armbian saja yang bisa di coba, Manjaro, Arch Linux, Artix Linux juga bisa di jalankan di STB Ex Indihome tersebut.

Preview nya bisa di cek langsung ke : [SINI](https://postimg.cc/gallery/S2XM9vJ)

### [Tutorial Instalasi](#tutorial-instalasi)

Untuk tutorial penginstalan, akan gw buatin satu satu :

- Install Armbian STB HG680P & B860H : _coming soon_
- Install Manjaro STB HG680P & B860H : _coming soon_
- Install Arch Linux STB HG680P & B860H : _coming soon_
- Install Artix Linux HG680P & B860H : _coming soon_

## [Kesimpulan](#kesimpulan)

Dan gw rasa udah cukup soal tulisan Single Board Computer Bagi Kaum Kere Hore ini, gw berharap bisa memberi gambaran keinginan anda para kaum seperti saya yang ingin memiliki SBC (Single Board Computer) tapi ga ada duit, maka belilah STB Ex Indihome HG680P & B860H terus di oprek.

Sekian, semoga bermanfaat & terima kasih :D
