---
slug: koneksi-wifi-dengan-terminal
title: Koneksi WiFi Dengan Terminal Linux
description: Tutorial lengkap cara mengkoneksikan WiFi dengan terminal di sistem operasi Linux tanpa GUI
date: 2019-05-15
author: Tanio
tags: ["tutorial", "linux", "network", "wifi", "terminal"]
featured: false
editable: true
---

<hr />

## [Introduction](#introduction)

Terkadang jika kita memanajemen server tanpa GUI, kita dituntut untuk mengoperasikan terminal. Lalu bagaimana jika server tidak menggunakan LAN tapi menggunakan WiFi adapter?

<br />

Pembahasan kali ini yaitu tentang cara simple mengkoneksikan wifi di sistem operasi Linux dengan terminal atau console.

<br />

Walau Linux telah dilengkapi dengan network manager berbentuk GUI, namun untuk keadaan tertentu (perbaikan/linux server) kamu hanya bisa setting jaringan Linux melalui terminal/shell.

<br />

## [Dependencies](#dependencies)

Dependensi yang harus dipenuhi yaitu:

- **iwconfig iwlist** - untuk scanning dan konfigurasi interface wireless
- **wpa_supplicant** - untuk menangani WPA/WPA2 authentication
- **wpa_passphrase** - untuk generate konfigurasi WPA
- **dhcpcd** atau **dhcpclient** - untuk mendapatkan IP address

<br />

## [Scan SSID](#scan-ssid)

Untuk scanning SSID kita bisa menggunakan `iwlist` dengan perintah:

```shell
root@ibislinux [ ~ ]# iwlist wlp2s0 scan | grep SSID
                      ESSID:"tethering"
                      ESSID:"PROGRAM"
                      ESSID:"New Office"
```

**Note**: _wlp2s0 merupakan nama interface wireless saya, jadi kalian bisa mengganti dengan interface wireless masing-masing_

<br />

Secara opsional, kalian bisa memunculkan data lengkap, misal kita ingin mengetahui data SSID dari `PROGRAM` dengan perintah:

```shell
iwlist wlp2s0 scan essid "PROGRAM"
```

<br />

## [Koneksi Tanpa Password](#koneksi-tanpa-password)

Untuk WiFi yang tidak menggunakan password, kita menggunakan `iwconfig` untuk mengkoneksikan SSID:

```shell
iwconfig wlp2s0 essid "PROGRAM"
```

Lalu request IP dari wireless dengan `dhcpcd`:

```shell
dhcpcd wlp2s0
```

Cek apakah kita sudah mendapatkan IP dengan `ifconfig`:

```shell
root@ibislinux [ ~ ]# ifconfig wlp2s0
wlp2s0    Link encap:Ethernet  HWaddr xx:xx:Xx:xx:xx
          inet addr:192.168.1.25  Bcast:192.168.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:75413 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6820 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:12439549  TX bytes:1132541
```

<br />

## [Koneksi Menggunakan Password](#koneksi-menggunakan-password)

Setelah mendapat target, kita generate file konfigurasi wireless nya yang berisi **SSID** dan password menggunakan `wpa_passphrase`. Kalian bisa menaruh file nya di mana saja:

```shell
wpa_passphrase "PROGRAM" "12312345678" > ~/.config/wpa/program.conf
```

<br />

Berikut contoh isi file konfigurasi:

```shell
cat ~/.config/wpa/program.conf
network={
	ssid="PROGRAM"
	#psk="12312345678"
	psk=e8bd99a04c19a9e5842cb9cc4c8883e2208134e369d2571bd3590ec63ef6913f
}
```

<br />

Selanjutnya yaitu mengkoneksikan komputer dengan wireless:

```shell
root@ibislinux [ ~ ]# wpa_supplicant -c ~/.config/wpa/program.conf -i wlp2s0 -D wext -B
```

**Catatan**: Sesuaikan nama file dan nama interface wireless kalian.

<br />

Setelah sukses, kita request IP dari wifi dengan perintah:

```shell
dhcpcd wlp2s0
```

<br />

Cek apakah kita sudah mendapatkan IP dengan `ifconfig`:

```shell
root@ibislinux [ ~ ]# ifconfig wlp2s0
wlp2s0    Link encap:Ethernet  HWaddr xx:xx:Xx:xx:xx
          inet addr:192.168.1.25  Bcast:192.168.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:75413 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6820 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:12439549  TX bytes:1132541
```

<br />

## [Conclusion](#conclusion)

Connecting to WiFi via terminal sangat berguna untuk server management atau troubleshooting networking issues. Method ini juga berguna ketika GUI tidak tersedia atau tidak berjalan dengan baik pada sistem Linux.

<br />

**Tips**: Selalu gunakan interface wireless yang sesuai dengan sistem Anda, dan pastikan semua dependencies sudah terinstall dengan benar.
