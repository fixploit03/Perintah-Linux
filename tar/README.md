# tar

## Apa itu tar?

`tar` adalah singkatan dari Tape Archive, sebuah perintah di Linux/Unix yang digunakan untuk:
- Menggabungkan banyak file/direktori menjadi satu file arsip (archive).
- Membongkar (extract) file arsip.
- Mengompresi atau mendekompresi arsip dengan bantuan program kompresi lain seperti `gzip`, `bzip2`, atau `xz`.

> Catatan: `tar` sendiri hanya mengarsipkan, bukan mengompresi. Tapi biasanya dipadukan dengan `gzip/bzip2/xz` untuk menghasilkan file `.tar.gz`, `.tar.bz2`, `.tar.xz`.

## Struktur Dasar Perintah tar

Format umum:

```
tar [opsi] [arsip] [file/direktori]
```

Keterangan:
- `[opsi]` -> menentukan tindakan (`c`=create, `x`=extract, `t`=list, dll.)
- `[arsip]` -> nama file arsip yang dibuat/dibuka.
- `[file/direktori]` -> file atau folder yang akan diarsipkan/ekstrak.

## Opsi Dasar tar yang Paling Penting

Beberapa opsi utama yang wajib diingat:

| Opsi | Nama | Fungsi |
|:--:|:--:|:--:|
| `-c` | create | Membuat arsip baru |
| `-x` | extract | Mengekstrak arsip |
| `-t` | list | Melihat isi arsip tanpa mengekstrak |
| `-f` | file | Menentukan nama file arsip |
| `-v` | verbose | Menampilkan proses secara detail |
| `-z` | gzip | Mengompresi/dekompresi dengan gzip (`.tar.gz`) |
| `-j` | bzip2 | Mengompresi/dekompresi dengan bzip2 (`.tar.bz2`) |
| `-J` | xz | Mengompresi/dekompresi dengan xz (`.tar.xz`) |
| `-C` | change dir | Mengekstrak ke direktori tertentu |
| `--wildcards` | wildcard | Menyaring file saat ekstrak dengan pola |

## Membuat Arsip

### 1. Membuat arsip sederhana

```
tar -cvf arsipku.tar file1 file2 dir1
```

Keterangan:
- `-c` : buat arsip
- `-v` : tampilkan proses
- `-f` : nama file arsip

Hasil: arsipku.tar

### 2. Membuat arsip terkompresi

#### a. gzip

```
tar -czvf arsipku.tar.gz file1 file2 dir1
```

#### b. bzip2

```
tar -cjvf arsipku.tar.bz2 file1 file2 dir1
```

#### c. xz

```
tar -cJvf arsipku.tar.xz file1 file2 dir1
```

## Mengekstrak Arsip

### 1. Ekstrak arsip .tar

```
tar -xvf arsipku.tar
```

### 2. Ekstrak arsip .tar.gz

```
tar -xzvf arsipku.tar.gz
```

### 3. Ekstrak arsip .tar.bz2

```
tar -xjvf arsipku.tar.bz2
```

### 4. Ekstrak arsip .tar.xz

```
tar -xJvf arsipku.tar.xz
```

### 5. Ekstrak ke direktori tertentu

```
tar -xvf arsipku.tar -C /path/tujuan/
```

## Melihat Isi Arsip Tanpa Ekstrak

```
tar -tvf arsipku.tar
```

Menampilkan daftar file di dalam arsip.

## Menambahkan File ke Arsip

```
tar -rvf arsipku.tar file_baru.txt
```

`-r` = append file ke dalam arsip (hanya bisa untuk `.tar`, bukan `.tar.gz`).

## Mengekstrak File Tertentu

```
tar -xvf arsipku.tar file1.txt file2.txt
```

## Menggunakan Wildcards

```
tar -xvf arsipku.tar --wildcards '*.txt'
```

Mengekstrak hanya file dengan ekstensi `.txt`.

## Praktik Lanjutan

### 1. Split (membagi arsip besar jadi beberapa bagian)

```
tar -czvf - folderku | split -b 100M - arsipku.tar.gz.part-
```

### 2. Extract dari stdin

```
cat arsipku.tar.gz | tar -xzvf -
```

### 3. Backup seluruh sistem (hati-hati, butuh root)

```
tar -cvpzf backup-system.tar.gz --exclude=/proc --exclude=/tmp --exclude=/mnt --exclude=/dev /
```

## Ekstensi yang Umum

- `.tar` -> hanya arsip
- `.tar.gz` -> arsip + gzip
- `.tar.bz2` -> arsip + bzip2
- `.tar.xz` -> arsip + xz

## Tips Penting
- Jangan lupa `-f` harus terakhir sebelum nama file arsip.
- Gunakan `-v` untuk belajar agar terlihat prosesnya.
- Untuk arsip besar, gunakan `-C` supaya rapi.
- Arsip `.tar.gz` lebih cepat tapi ukuran agak besar. `.tar.xz` lebih kecil tapi lebih lambat.

## Contoh Lengkap Step by Step

### 1. Buat folder data:

```
mkdir data
echo "halo" > data/file1.txt
echo "belajar tar" > data/file2.txt
```

### 2. Arsipkan:

```
tar -czvf data.tar.gz data/
```

### 3. Lihat isi arsip:

```
tar -tvf data.tar.gz
```

### 4. Ekstrak ke folder lain:

```
tar -xzvf data.tar.gz -C /tmp
```

Selesai :)
