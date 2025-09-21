# grep

## A. Apa itu grep?

`grep` adalah singkatan dari "Global Regular Expression Print". Ini adalah perintah yang sangat powerful di Linux/Unix untuk mencari teks atau pola tertentu dalam file atau output perintah lain.

## B. Fungsi Utama grep:

- Mencari baris yang mengandung pola tertentu
- Memfilter output dari perintah lain
- Mencari dalam satu atau multiple file
- Menggunakan regular expression untuk pencarian kompleks

## C. Sintaks Dasar

```
grep [OPTION] PATTERN [FILE...]
```

**Komponen:**

- **OPTION:** Flag atau parameter tambahan
- **PATTERN:** Teks atau pola yang dicari
- **FILE:** File tempat pencarian (opsional, bisa dari stdin)

## D. Penggunaan Dasar

### 1. Mencari Teks Sederhana

```
# Mencari kata "hello" dalam file.txt
grep "hello" file.txt

# Mencari dalam multiple file
grep "hello" file1.txt file2.txt file3.txt

# Mencari dalam semua file .txt
grep "hello" *.txt
```

### 2. Menggunakan dengan Pipe

```
# Mencari proses yang mengandung "apache"
ps aux | grep apache

# Mencari file yang mengandung "config"
ls -la | grep config

# Mencari dalam output perintah lain
cat /etc/passwd | grep root
```

### 3. Contoh Output

```
$ grep "root" /etc/passwd
root:x:0:0:root:/root:/bin/bash
operator:x:11:0:operator:/root:/sbin/nologin
```

## E. Option-option Penting

### Option Dasar

#### 1. `-i` (ignore case)

Mengabaikan perbedaan huruf besar/kecil.

```
grep -i "hello" file.txt
```

Akan menemukan: `hello`, `Hello`, `HELLO`, `HeLLo` di dalam file `file.txt`.

#### 2. `-v` (invert match)

Menampilkan baris yang TIDAK mengandung pola.

```
grep -v "comment" config.txt
```

Menampilkan semua baris kecuali yang mengandung `comment` di dalam file `config.txt`.

#### 3. `-n` (line number)

Menampilkan nomor baris.

```
grep -n "error" log.txt
```

Output: 15:Error occurred at startup


#### 4. `-c` (count)

Menghitung jumlah baris yang cocok.

```
grep -c "warning" log.txt
```

Output: `23`

#### 5. `-l` (files with matches)

Menampilkan nama file yang mengandung pola.

```
grep -l "TODO" *.py
```

Output:

```
main.py
run.py
script.py
```

#### 6. `-L` (files without matches)

Menampilkan nama file yang TIDAK mengandung pola.

```
grep -L "TODO" *.py
```

Output:

```
config.py
install.py
setup.py
```
