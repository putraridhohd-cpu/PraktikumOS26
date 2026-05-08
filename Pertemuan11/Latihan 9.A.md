# Latihan 9.A — Audit dan Kolaborasi

## Langkah 1: Menemukan File SUID Aktif
Gunakan perintah ini untuk mendeteksi file yang memiliki bit SUID:
```
find / -perm -4000 -type f 2>/dev/null | head -n 20
```
<img width="445" height="221" alt="image" src="https://github.com/user-attachments/assets/ba71f935-6da6-40f0-8c4d-7840deecc6b7" />

Permisi SUID membuat user biasa menjalankan file itu dengan otoritas pemiliknya (biasanya pake root).
di output gambar ada file seperti yang dikotaki di daftar paling atas. File ini wajib punya SUID agar user biasa bisa ganti password atau meminta hak akses admin.

## Langkah 2: Mencari Direktori World-Writable
Gunakan perintah ini untuk mencari direktori yang bisa ditulis oleh siapa pun:
```
find / -type d -perm -0002 2>/dev/null
```
<img width="606" height="338" alt="image" src="https://github.com/user-attachments/assets/f7fdadc9-40f6-440d-b00a-23499ff21a3b" />
Muncul direktori kayak /tmp dan /var/tmp. Ini adalah direktori valid karena butuh sistem buat simpan file sementara,tapi bisa berisiko kalau ada direktori sensitif lain yang memiliki permisi serupa tanpa pengawasan.

## Langkah 3: Konfigurasi Permission Standar dan ACL
Berikut adalah rangkaian kode untuk mengatur kolaborasi pada direktori /srv/webapp/:
### 1. buat direktori dan group jika belum ada dan atur permission standar & SetGID
<img width="1024" height="186" alt="image" src="https://github.com/user-attachments/assets/b86f71a3-c7cb-442d-8c99-61d8493a7c13" />

### 2. Mengatur ACL untuk user deploy
kita  buat dulu user deploy nya,lalu jalankan perintah ini:
<img width="617" height="39" alt="image" src="https://github.com/user-attachments/assets/217be1ce-3ebe-4819-ad9a-52603a1b215c" />

## Langkah 4. Kita verifikasi hasilnya:
<img width="600" height="285" alt="image" src="https://github.com/user-attachments/assets/42b32408-ace0-435f-9b89-3010e718eb6f" />

Baris user yang sudah saya kotaki membuktikan kalau user deploy sekarang sudah ada hak akses khusus untuk membaca dan masuk ke direktori itu tapi gak bisa mengubah isinya
