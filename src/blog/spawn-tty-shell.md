---
slug: spawn-tty-shell
title: Spawn TTY Shell
description: Beberapa cara spawn/memunculkan TTY Shell untuk penetration testing
date: 2019-04-28
author: Rahul
tags: ["tutorial", "tty", "shell", "pentest", "linux"]
featured: false
editable: true
---

<hr />

## [Introduction](#introduction)

Seringkali selama _pentest_ Anda dapat memperoleh _shell_ tanpa _tty_, namun ingin berinteraksi lebih jauh dengan sistem. Berikut adalah beberapa perintah yang akan memungkinkan Anda untuk memanggil _shell_ _tty_.

Jelas beberapa hal ini akan tergantung pada lingkungan sistem dan paket yang diinstal.

## [Shell Spawning](#shell-spawning)

### [Python](#python)

```bash
python -c 'import pty; pty.spawn("/bin/sh")'
```

### [Perl](#perl)

```bash
perl —e 'exec "/bin/sh";'
```

### [Ruby](#ruby)

```bash
exec "/bin/sh"
```

### [Echo](#echo)

```bash
echo os.system('/bin/bash')
```

### [Shell](#shell)

```bash
/bin/sh -i
```

### [Lua](#lua)

```bash
os.execute('/bin/sh')
```

### [From within IRB](#from-within-irb)

```bash
exec "/bin/sh"
```

### [From within vi](#from-within-vi)

```bash
:!bash #atau :set shell=/bin/bash:shell
```

### [From within nmap](#from-within-nmap)

```bash
!sh
```

## [Kesimpulan](#kesimpulan)

**3 teratas** adalah perintah yang kebanyakan sukses di gunakan untuk spawning tty shell. Selamat mencoba.
