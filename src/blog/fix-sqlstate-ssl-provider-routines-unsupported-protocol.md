---
slug: fix-ssl-provider-error-unsupported-protocol
title: Fix SQL Server SSL Provider [SSL routines::unsupported protocol]
description: Sharing pengalaman troubleshooting error SSL routines::unsupported protocol saat koneksi ke Microsoft SQL Server di Ubuntu 22.04 dan 24.04.
date: 2026-02-15
author: Tanio
tags:
  [
    "tutorial",
    "linux",
    "ubuntu",
    "sqlserver",
    "ssl",
    "php",
    "laravel",
    "database",
  ]
featured: true
editable: false
---

<hr />

## [Intro](#intro)

Artikel ini membahas penyelesaian masalah koneksi database Microsoft SQL Server yang menghasilkan error:

```
SSL Provider: [SSL routines::unsupported protocol]
```

Error ini umumnya terjadi karena perbedaan versi protokol SSL/TLS antara _client_ dan _server_, atau karena konfigurasi _security level_ yang terlalu ketat pada sistem operasi yang lebih baru.

## [Masalah](#masalah)

Ketika mencoba melakukan koneksi ke database Microsoft SQL Server, Anda akan mendapatkan error yang mirip seperti ini:

![Error SSL Provider Screenshot](/images/ssl-routines-unsupported-protocol.png)

Error ini dapat muncul pada berbagai aplikasi yang menggunakan koneksi database, seperti:

- Aplikasi _Laravel/PHP_
- _Tools database management_
- _Script custom_ yang menggunakan _ODBC/FreeTDS_

## [Akar Masalah](#root-cause)

Error `SSL routines::unsupported protocol` disebabkan oleh:

1. **Security Level yang Terlalu Tinggi**: Versi Ubuntu yang lebih baru memiliki _default security level_ yang lebih ketat
2. **Kompatibilitas Protocol**: Microsoft SQL Server versi lama menggunakan protokol SSL/TLS yang sudah _deprecated_
3. **Konfigurasi OpenSSL**: Pengaturan _cipher string_ yang tidak kompatible

## [Ubuntu 22.04](#ubuntu-22-04-solution)

### [Environment](#environment-22-04)

Alat dan bahan yang digunakan:

- **OS**: Ubuntu 22.04
- **PHP**: 8.3
- **Database**: Microsoft SQL Server 2014 - 12.0.2000.8 (X64)
- **Framework**: Laravel 12

### [Langkah Langkah](#langkah-langkah-22-04)

1. **Buka file konfigurasi OpenSSL**:

   ```bash
   sudo nano /etc/ssl/openssl.cnf
   ```

2. **Cari bagian CipherString**:

   ![OpenSSL Config Before Ubuntu 22.04](/images/fix-ssl-sqlserver-ubuntu-2204.jpg)

3. **Ubah nilai CipherString**:
   Ganti dari:

   ```
   CipherString = DEFAULT@SECLEVEL=2
   ```

   Menjadi:

   ```
   CipherString = DEFAULT@SECLEVEL=0
   ```

4. **Simpan dan restart service**:

   ```bash
   sudo systemctl restart apache2
   # atau
   sudo systemctl restart nginx
   ```

### [Mengapa Ini Bekerja](#mengapa-ini-bekerja-22-04)

Mengubah `SECLEVEL=2` ke `SECLEVEL=0` akan:

- Menurunkan tingkat keamanan OpenSSL dari level 2 ke level 0
- Mengizinkan penggunaan algoritma enkripsi yang lebih lama
- Memungkinkan koneksi ke server SSL yang menggunakan protokol _deprecated_

⚠️ **Catatan Keamanan**: Solusi ini menurunkan level keamanan SSL. Pastikan jaringan Anda aman dan pertimbangkan untuk _upgrade_ SQL Server jika memungkinkan.

## [Ubuntu 24.04](#ubuntu-24-04-solution)

### [Environment](#environment-24-04)

Alat dan bahan yang digunakan:

- **OS**: Ubuntu 24.04
- **PHP**: 8.3
- **Database**: Microsoft SQL Server 2014 - 12.0.2000.8 (X64)

### [Langkah Langkah](#langkah-langkah-24-04)

1. **Buka file konfigurasi OpenSSL**:

   ```bash
   sudo nano /etc/ssl/openssl.cnf
   ```

2. **Scroll ke bagian paling bawah file**:

   ![OpenSSL Config Before Ubuntu 24.04](/images/fix-ssl-sqlserver-ubuntu-2404.jpg)

3. **Tambahkan konfigurasi berikut di bagian paling bawah**:

   ```ini
   [ssl_sect]
   system_default = system_default_sect

   [system_default_sect]
   CipherString = DEFAULT:@SECLEVEL=0
   ```

4. **Konfigurasi akhir akan terlihat seperti ini**:

   ![OpenSSL Config After Ubuntu 24.04](/images/fix-ssl-sqlserver-ubuntu-2404.jpg)

5. **Simpan file dan restart service**:

   ```bash
   sudo systemctl restart apache2
   # atau
   sudo systemctl restart nginx
   ```

### [Mengapa Ini Bekerja](#mengapa-ini-bekerja-24-04)

Pada Ubuntu 24.04, konfigurasi OpenSSL menggunakan _section-based configuration_ yang lebih terstruktur. Dengan menambahkan section `[ssl_sect]` dan `[system_default_sect]`, kita:

- Membuat konfigurasi SSL yang spesifik untuk sistem
- Mengatur CipherString dengan SECLEVEL=0 secara terpisah
- Mempertahankan kompatibilitas dengan konfigurasi OpenSSL yang lebih baru

## [Verifikasi](#verifikasi)

Setelah menerapkan salah satu solusi di atas, Anda dapat memverifikasi koneksi dengan cara:

### [Testing Sederhana](#testing-sederhana)

```php
<?php
try {
    $serverName = "your-server-ip";
    $connectionOptions = [
        "Database" => "your_database",
        "Uid" => "your_username",
        "PWD" => "your_password",
        "Encrypt" => true,
        "TrustServerCertificate" => true
    ];

    $conn = sqlsrv_connect($serverName, $connectionOptions);

    if ($conn) {
        echo "Connection successful!";
    } else {
        print_r(sqlsrv_errors());
    }
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
?>
```

## [Troubleshooting Tambahan](#troubleshooting-tambahan)

### [Jika Masih Bermasalah](#jika-masih-bermasalah)

1. **Restart sistem** setelah mengubah konfigurasi OpenSSL
2. **Periksa log error**:

   ```bash
   tail -f /var/log/apache2/error.log
   # atau
   tail -f /var/log/nginx/error.log
   ```

3. **Verifikasi konfigurasi OpenSSL**:

   ```bash
   openssl version -a
   ```

4. **Test koneksi dengan telnet**:
   ```bash
   telnet your-server-ip 1433
   ```

### [Other Possible Errors](#other-possible-errors)

- **Certificate verification failed**: Tambahkan `TrustServerCertificate=true` pada _connection string_
- **Login timeout expired**: Periksa _firewall_ dan _network connectivity_
- **Protocol version not supported**: Pastikan SQL Server support TLS 1.0+

## [Konklusi](#konklusi)

Error SSL Provider `SSL routines::unsupported protocol` dapat diatasi dengan menurunkan _security level_ OpenSSL. Meski solusi ini efektif, penting untuk mempertimbangkan implikasi keamanan dan jika memungkinkan, lakukan _upgrade_ pada SQL Server untuk mendukung protokol SSL/TLS yang lebih modern.

**Ringkasan Solusi**:

- **Ubuntu 22.04**: Ubah `CipherString = DEFAULT@SECLEVEL=2` menjadi `CipherString = DEFAULT@SECLEVEL=0`
- **Ubuntu 24.04**: Tambahkan section SSL configuration baru dengan `CipherString = DEFAULT:@SECLEVEL=0`

Kedua solusi telah ditest dan berfungsi dengan baik pada _environment_ yang disebutkan di atas.

## [Catatan](#catatan)

_Artikel ini berdasarkan pengalaman troubleshooting pada environment production. Selalu lakukan backup konfigurasi sebelum melakukan perubahan._

## [Referensi](#referensi)

1. [[Microsoft][ODBC Driver 17 for SQL Server]SSL Provider: [error:1425F102:SSL routines:ssl_choose_client_version:unsupported protocol]](https://github.com/microsoft/msphpsql/issues/1112)
2. [SQLSTATE[08001]: [Microsoft][ODBC Driver 18 for SQL Server]SSL Provider: [error:0A000102:SSL routines::unsupported protocol]](https://github.com/microsoft/msphpsql/issues/1462)
