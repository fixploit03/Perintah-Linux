# chmod

## A. Apa itu chmod?

`chmod` adalah singkatan dari "Change Mode". Ini adalah perintah fundamental di Linux/Unix untuk mengubah permissions (izin akses) file dan direktori.

## B. Fungsi Utama chmod:

- Mengatur siapa yang bisa membaca (read) file/direktori
- Mengatur siapa yang bisa menulis (write) file/direktori
- Mengatur siapa yang bisa menjalankan (execute) file/direktori
- Mengontrol keamanan sistem file

## C. Mengapa chmod Penting?

- **Keamanan:** Melindungi file sensitif dari akses tidak sah
- **Privacy:** Mengatur file pribadi agar tidak bisa dibaca orang lain
- **Functionality:** Membuat script bisa dijalankan
- **System Administration:** Mengatur akses sistem secara proper

## D. Konsep File Permissions di Linux

### Tiga Jenis Permission:

- Read (`r`): Izin untuk membaca file atau melihat isi direktori
- Write (`w`): Izin untuk menulis/mengubah file atau menambah/hapus file dalam direktori
- Execute (`x`): Izin untuk menjalankan file atau masuk ke direktori

### Tiga Kategori User:

- Owner (`u`): Pemilik file/direktori
- Group (`g`): Grup yang memiliki file/direktori
- Others (`o`): User lain di sistem

## E. Melihat Permissions

```
ls -l file.txt
```

Output:

```
-rwxr-xr-- 1 fixploit03 fixploit03 1568 Sep 21 19:46 file.txt
```

## F. Format Output:

```
-rwxr-xr--
│└┬┘└┬┘└┬┘
│ │  │  └── Others permissions (r--)
│ │  └───── Group permissions (r-x)  
│ └──────── Owner permissions (rwx)
└────────── File type (- = file, d = directory)
```

## G. Memahami Permission Format

### Representasi Huruf:

- `r` = Read (4 dalam nilai numerik)
- `w` = Write (2 dalam nilai numerik)
- `x` = Execute (1 dalam nilai numerik)
- `-` = Tidak ada permission (0 dalam nilai numerik)

### Contoh Interpretasi:

```
-rwxr-xr--
```

- **File type:** `-` (regular file)
- **Owner:** `rwx` (read + write + execute = 7)
- **Group:** `r-x` (read + execute = 5)
- **Others:** `r--` (read only = 4)
- **Numerik:** 754

## H. Sintaks chmod

### 1. Sintaks Dasar:

```
chmod [OPTION] MODE FILE...
```

**Komponen:**

- **OPTION:** Parameter tambahan (seperti `-R` untuk recursive)
- **MODE:** Permission yang ingin diset (numerik atau simbolik)
- **FILE:** File atau direktori target

## I. Metode Numerik (Octal)

### Sistem Octal (Base 8):

Menggunakan angka `0-7` untuk merepresentasikan kombinasi permissions.

**Nilai Dasar:**

- `4` = Read (`r`)
- `2` = Write (`w`)
- `1` = Execute (`x`)
- `0` = No permission (`-`)

## J. Kombinasi Umum:

```
7 = 4+2+1 = rwx (read + write + execute)
6 = 4+2+0 = rw- (read + write)
5 = 4+0+1 = r-x (read + execute)
4 = 4+0+0 = r-- (read only)
3 = 0+2+1 = -wx (write + execute) [jarang digunakan]
2 = 0+2+0 = -w- (write only) [jarang digunakan]
1 = 0+0+1 = --x (execute only)
0 = 0+0+0 = --- (no permission)
```

## K. Format Tiga Digit:

```
chmod ABC file
```

- `A` = Owner permissions
- `B` = Group permissions  
- `C` = Others permissions

## L. Contoh Penggunaan Numerik:

```
# 755: Owner=rwx, Group=r-x, Others=r-x
chmod 755 script.sh

# 644: Owner=rw-, Group=r--, Others=r--
chmod 644 document.txt

# 700: Owner=rwx, Group=---, Others=---
chmod 700 private_script.sh

# 666: Owner=rw-, Group=rw-, Others=rw-
chmod 666 shared_file.txt

# 777: Owner=rwx, Group=rwx, Others=rwx (HATI-HATI!)
chmod 777 file.txt
```

## M. Tabel Referensi Cepat:

| Permission  | Numerik | Simbolik
|:--:|:--:|:--:|
| No access | 0 | `---` |
| Execute | 1 | `--x` |
| Write | 2 | `--x` |
| Write+Exec | 3 | `-wx` |
| Read | 4 | `r--` |
| Read+Exec | 5 | `r-x` |
| Read+Write | 6 | `rw-` |
| Full access | 7 | `rwx` |


## N. Metode Simbolik

### Format Simbolik:

```
chmod [ugoa][+-=][rwx] file
```

**Komponen:**

- `[ugoa]`: Target (user/owner, group, others, all)
- `[+-=]`: Operasi (tambah, kurang, set)
- `[rwx]`: Permission yang diubah

**Target (Who):**

- `u`: user/owner
- `g`: group
- `o`: others
- `a`: all (u+g+o)

**Operasi (Operator):**

- `+`: Menambah permission
- `-`: Menghapus permission
- `=`: Set permission (mengganti semua)

**Permission:**

- `r`: read
- `w`: write
- `x`: execute

## O. Contoh Simbolik:

```
# Menambah execute permission untuk owner
chmod u+x script.sh

# Menghapus write permission untuk group dan others
chmod go-w file.txt

# Set read+write untuk owner, read untuk group, tidak ada untuk others
chmod u=rw,g=r,o= file.txt

# Menambah read permission untuk semua
chmod a+r document.txt

# Menghapus execute permission untuk others
chmod o-x script.sh

# Multiple operations sekaligus
chmod u+rw,g+r,o-rwx file.txt
```

## P. Option-option chmod

### 1. `-R` atau `--recursive`

Mengubah permission secara rekursif (untuk direktori dan semua isi di dalamnya).

```
chmod -R 755 /path/to/directory/
chmod -R u+x /path/to/scripts/
```

### 2. `-v` atau `--verbose`

Menampilkan informasi detail tentang perubahan yang dilakukan.

```
hchmod -v 644 file.txt
```

Output: mode of 'file.txt' changed from 0755 (rwxr-xr-x) to 0644 (rw-r--r--)

### 3. `-c` atau `--changes`

Hanya menampilkan file yang benar-benar berubah.

```
chmod -c 644 *.txt
```

### 4. `--reference=RFILE`

Menggunakan permission dari file lain sebagai referensi.

```
chmod --reference=template.txt newfile.txt
```

### 5. `--preserve-root`

Mencegah operasi rekursif pada root directory (keamanan).

```
chmod --preserve-root -R 777 /
```

## Q. Contoh Praktis

### 1. Script dan Executable Files

```
# Membuat script executable
chmod +x script.sh
chmod 755 script.sh

# Script hanya untuk owner
chmod 700 private_script.sh

# Script yang bisa dibaca semua tapi hanya owner yang execute
chmod 644 script.sh
chmod u+x script.sh
```

### 2. File Dokumen

```
# Dokumen standar: owner read/write, others read-only
chmod 644 document.txt

# Dokumen privat: hanya owner yang bisa akses
chmod 600 private_document.txt

# Dokumen shared: semua bisa read/write
chmod 666 shared_document.txt
```

### 3. Direktori

```
# Direktori standar: owner full access, others read+execute
chmod 755 /path/to/directory/

# Direktori privat: hanya owner
chmod 700 /path/to/private_dir/

# Direktori public: semua bisa akses
chmod 755 /path/to/public_dir/

# Set permission rekursif untuk web directory
chmod -R 644 /var/www/html/
find /var/www/html/ -type d -exec chmod 755 {} \;
```

### 4. Kasus Web Development

```
# WordPress typical permissions
find /var/www/wordpress/ -type f -exec chmod 644 {} \;
find /var/www/wordpress/ -type d -exec chmod 755 {} \;
chmod 600 /var/www/wordpress/wp-config.php
```

### 5. Backup dan Log Files

```
# Log files: owner write, group read, others no access
chmod 640 /var/log/application.log

# Backup files: owner only
chmod 600 backup.tar.gz

# Temporary files
chmod 644 /tmp/tempfile.txt
```

## R. Special Permissions

### 1. Setuid (Set User ID) - 4

File dijalankan dengan permission owner, bukan user yang menjalankan.

```
chmod 4755 program
chmod u+s program

# Contoh: passwd command
ls -l /usr/bin/passwd
# -rwsr-xr-x (perhatikan 's' di posisi execute owner)
```

### 2. Setgid (Set Group ID) - 2

File dijalankan dengan permission group, atau file baru dalam direktori mengikuti group direktori.

```
chmod 2755 directory
chmod g+s directory

# Untuk file
chmod 2755 program

# Untuk direktori: file baru akan mengikuti group direktori
chmod g+s /shared/directory/
```

### 3. Sticky Bit - 1

Hanya owner file yang bisa menghapus file dalam direktory (biasanya untuk /tmp).

```
chmod 1755 directory
chmod +t directory

# Contoh: /tmp directory
ls -ld /tmp
# drwxrwxrwt (perhatikan 't' di akhir)
```

### 4. Kombinasi Special Permissions

```
# Format: SABC dimana S=special permissions (4+2+1)
chmod 4755 file  # setuid + 755
chmod 2755 dir   # setgid + 755  
chmod 1755 dir   # sticky + 755
chmod 6755 file  # setuid+setgid + 755
chmod 7755 dir   # setuid+setgid+sticky + 755
```

## S. Best Practices

### 1. Prinsip Least Privilege

Berikan permission minimum yang dibutuhkan.

```
# BAIK: Dokumen standar
chmod 644 document.txt

# BURUK: Terlalu permissive
chmod 777 document.txt
```

### 2. Permission untuk Berbagai Jenis File

```
# Executable scripts
chmod 755 script.sh

# Configuration files  
chmod 644 config.conf

# Private keys
chmod 600 private_key.pem

# Public keys
chmod 644 public_key.pub

# Log files
chmod 644 application.log
```

### 3. Web Server Permissions

```
# HTML/CSS/JS files
chmod 644 *.html *.css *.js

# PHP files
chmod 644 *.php

# Upload directories
chmod 755 uploads/

# Configuration files
chmod 600 config.php
```

### 4. Backup dan Security

```
# Backup files - owner only
chmod 600 backup.tar.gz

# System configuration
chmod 644 /etc/config.conf

# Sensitive files
chmod 600 /etc/shadow
chmod 600 ~/.ssh/id_rsa
```

## T. Troubleshooting

### 1. Permission Denied Errors

```
# Problem: Cannot execute script
# Solution:
chmod +x script.sh

# Problem: Cannot write to file
# Solution:
chmod u+w filename

# Problem: Cannot access directory
# Solution:
chmod u+x directory/
```

### 2. Web Server Issues

```
# Problem: 403 Forbidden
# Check: File dan directory permissions
chmod 644 index.html
chmod 755 /var/www/html/

# Problem: Cannot write uploads
# Solution:
chmod 755 uploads/
# atau
chmod 777 uploads/ # Hati-hati dengan security!
```

### 3. Common Mistakes

```
# SALAH: Menghapus execute dari direktori
chmod 644 directory/
# FIX:
chmod 755 directory/

# SALAH: Membuat file terlalu permissive
chmod 777 config.php
# FIX:
chmod 644 config.php

# SALAH: Menghapus read permission dari file yang dibutuhkan
chmod 000 important_file.txt
# FIX:
chmod 644 important_file.txt
```
