# grep

![](https://github.com/fixploit03/Perintah-Linux/blob/main/grep/perintah%20grep.png)

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

Output: Akan menampilkan semua baris kecuali yang mengandung `comment` di dalam file `config.txt`.

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

### Option Lanjutan

#### 1. `-r` atau `-R` (recursive)

Mencari dalam direktori dan subdirektori.

```
# Mencari kata "function" secara rekursif di dalam direktori "/home/user/project/"
grep -r "function" /home/user/project/

# Mencari kata "import" secara rekursif di dalam direktori saat ini
grep -R "import" .
```

#### 2. `-w` (word boundary)

Mencari kata utuh, bukan sebagian kata.

```
grep -w "cat" file.txt
```

Output: Akan menemukan: `cat` tapi tidak `category` atau `concatenate`.

#### 3. `-x` (exact line)

Mencocokkan seluruh baris.

```
grep -x "exact line" file.txt
```

#### 4. `-A NUM` (after)

Menampilkan NUM baris setelah baris yang cocok.

```
grep -A 3 "error" log.txt
```

Output: Akan menampilkan baris `error + 3 baris berikutnya`.

#### 5. `-B NUM` (before)

Menampilkan NUM baris sebelum baris yang cocok.

```
grep -B 2 "error" log.txt
```

Output: Akan menampilkan `2 baris sebelum + baris error`.

#### 6. `-C NUM` (context)

Menampilkan NUM baris sebelum dan setelah.

```
grep -C 2 "error" log.txt
```

Output: Sama dengan `-A 2 -B 2`.

#### 7. `--color`

Mewarnai hasil pencarian.

```
grep --color=auto "pattern" file.txt
```

## F. Regular Expression dengan grep

### Metacharacters Dasar

#### 1. `.` (titik)

Mencocokkan karakter apapun.

```
grep "h.llo" file.txt
```

Output: Akan menemukan: `hello`, `hallo`, `hillo`.

#### 2. `^` (awal baris)


Mencocokkan awal baris.

```
grep "^root" /etc/passwd
```

Output: Akan menampilkan baris yang dimulai dengan `root`.

#### 3. `$` (akhir baris)

Mencocokkan akhir baris.

```
grep "bash$" /etc/passwd
```

Output: Akan menampilkan baris yang diakhiri dengan `bash`.

#### 4. `*` (nol atau lebih)

Mencocokkan nol atau lebih karakter sebelumnya.

```
grep "ab*c" file.txt
```

Output: Akan menemukan: `ac`, `abc`, `abbc`, `abbbc`.

#### 5. `[]` (character class)

Mencocokkan salah satu karakter dalam kurung.

```
grep "[aeiou]" file.txt          # Vokal
grep "[0-9]" file.txt            # Digit
grep "[A-Z]" file.txt            # Huruf besar
grep "[a-zA-Z0-9]" file.txt      # Alfanumerik
```

#### 6. `[^]` (negated character class)

Mencocokkan karakter yang TIDAK ada dalam kurung.

```
grep "[^0-9]" file.txt
```

Output: Akan menampilkan karakter non-digit.

### Extended Regular Expressions (grep -E atau egrep)

#### 1. `+` (satu atau lebih)

```
grep -E "ab+c" file.txt
```

Output: Akan menemukan: `abc`, `abbc`, `abbbc` (tapi tidak `ac`).

#### 2. `?` (nol atau satu)

```
grep -E "colou?r" file.txt
```

Output: Akan menemukan: `color`, `colour`.

#### 3. `|` (alternation)

```
grep -E "cat|dog" file.txt
```

Output: Akan menemukan baris dengan `cat` atau `dog`.

#### 4. `()` (grouping)

```
grep -E "(http|https)://.*" file.txt
```

Output: Akan menampilkan URL dengan protokol `http` atau `https`.

#### 5. `{n,m}` (quantifiers)

```
grep -E "[0-9]{3,5}" file.txt    # 3-5 digit
grep -E "[a-z]{4}" file.txt      # Tepat 4 huruf kecil
grep -E "[0-9]{3,}" file.txt     # Minimal 3 digit
```

### G. Contoh Pattern Berguna

```
# Email
grep -E "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" file.txt

# IP Address
grep -E "([0-9]{1,3}\.){3}[0-9]{1,3}" file.txt

# Nomor telepon (format: 08xx-xxxx-xxxx)
grep -E "08[0-9]{2}-[0-9]{4}-[0-9]{4}" file.txt

# Tanggal (format: DD/MM/YYYY)
grep -E "[0-3][0-9]/[0-1][0-9]/[0-9]{4}" file.txt
```

### H. Varian grep

#### 1. `egrep` (Extended grep)

Sama dengan `grep -E`.

```
egrep "pattern1|pattern2" file.txt
```

#### 2. `fgrep` (Fixed grep)

Sama dengan `grep -F`, tidak menggunakan regex.

```
fgrep "literal.string" file.txt
```

Output: Akan mencari `literal.string` secara literal (titik bukan wildcard).

#### 3. `rgrep`

Sama dengan `grep -r.

```
rgrep "pattern" directory/
```

### I. Contoh Kasus Praktis

#### 1. Analisis Log File

```
# Mencari error dalam log
grep -i "error" /var/log/apache2/error.log

# Mencari error pada tanggal tertentu
grep "2024-01-15" /var/log/syslog | grep -i error

# Menghitung jumlah error per hari
grep "2024-01-15" /var/log/apache2/error.log | grep -c "error"

# Mencari 404 errors dengan context
grep -C 3 "404" /var/log/apache2/access.log
```

#### 2. Konfigurasi System

```
# Mencari konfigurasi yang tidak di-comment
grep -v "^#" /etc/apache2/apache2.conf | grep -v "^$"

# Mencari user dengan shell bash
grep "bash$" /etc/passwd

# Mencari port yang listening
netstat -tuln | grep ":80 "
```

#### 3. Programming

```
# Mencari fungsi dalam kode Python
grep -n "def " *.py

# Mencari TODO comments
grep -r "TODO\|FIXME\|HACK" .

# Mencari import statements
grep -E "^(import|from)" *.py

# Mencari variabel global
grep -n "global " *.py
```

#### 4. File Management

```
# Mencari file yang mengandung teks tertentu
grep -l "database" *.conf

# Mencari file besar dalam output ls
ls -la | grep -E "^-.*[0-9]{7,}"

# Mencari file dengan ekstensi tertentu
ls -la | grep -E "\.(jpg|png|gif)$"
```

### J. Tips dan Trik

#### 1. Kombinasi dengan Perintah Lain

```
# Mencari proses dan kill
ps aux | grep apache | awk '{print $2}' | xargs kill

# Mencari dan menghitung file
find . -name "*.py" | xargs grep -l "import sys" | wc -l

# Pipeline kompleks
cat access.log | grep "404" | cut -d' ' -f1 | sort | uniq -c | sort -nr
```

#### 2. Menggunakan File Pattern

```
# Simpan pattern dalam file
echo -e "error\nwarning\nfatal" > patterns.txt
grep -f patterns.txt log.txt
```

#### 3. Output ke File

```
# Simpan hasil pencarian
grep "error" log.txt > errors.txt

# Append ke file
grep "warning" log.txt >> errors.txt
```

#### 4. Mencari Multiple Patterns

```
# OR condition
grep -E "pattern1|pattern2" file.txt

# AND condition (menggunakan pipeline)
grep "pattern1" file.txt | grep "pattern2"
```

#### 5. Performance Tips

```
# Gunakan -F untuk literal string (lebih cepat)
grep -F "exact.string" file.txt

# Gunakan -q untuk check existence saja
if grep -q "pattern" file.txt; then
    echo "Pattern found"
fi

# Limit pencarian dengan --max-count
grep --max-count=1 "pattern" file.txt
```
