# Praktikum 9.4 — Konfigurasi sudo
Tujuan: membuat aturan sudo terbatas, memverifikasi hak akses, dan membaca log.

## Langkah 1: Buat file konfigurasi sudo khusus untuk userA.
```
sudo visudo -f / etc / sudoers . d / lab - userA
```
lalu isi:
```
userA ALL=(root) NOPASSWD: /usr/bin/apt update, /usr/bin/apt upgrade
userA ALL=(root) /bin/systemctl status *
```

## Langkah 2: Verifikasi aturan yang aktif dan uji hasilnya.
<img width="950" height="341" alt="image" src="https://github.com/user-attachments/assets/b6d5da65-3ba7-4b51-a15c-c930e1e9a4bd" />

## analisis
### 1. Mengapa aturan disimpan di /etc/sudoers.d//, bukan langsung di /etc/sudoers?
biar lebih aman dan rapi karena memisahkan konfigurasi khusus user tertentu dalam file tersendiri tanpa mengganggu file utama sistem,jadinya risiko kerusakan pada konfigurasi sudo pusat bisa di minimalisir
<img width="952" height="68" alt="image" src="https://github.com/user-attachments/assets/77c33478-53b2-4749-a062-ed65f152efe3" />
ini berarti sistem mendukung pembuatan file konfigurasi terpisah yang bersifat spesifik dan modular.

### 2. Mana perintah yang bisa dijalankan tanpa password, dan mana yang masih perlu autentikasi?
Perintah apt update dan apt upgrade bisa dijalankan tanpa password,kalau systemctl status masih perlu autentikasi normal.
<img width="1813" height="241" alt="image" src="https://github.com/user-attachments/assets/e953e6a0-31ba-477a-abf2-42c7136b00b6" />
yang ada tulisan NOPASSWD berarti gak butuh password,begitupun sebaliknya

### 3. Informasi apa saja yang dicatat di log sudo?
Log itu mencatat secara detail siapa yang menjalankan perintah, terminal yang digunakan (TTY), lokasi direktori saat itu (PWD), identitas target (USER), hingga perintah spesifik yang dieksekusi.
<img width="947" height="52" alt="image" src="https://github.com/user-attachments/assets/e7f5b333-dadd-43bf-825c-8782b237b07b" />

* ridho26 (pelaku)
* TTY=pts/0 (jalur terminal)
* USER=root (dijalankan sebagai root)
* COMMAND=/usr/bin/grep userA /var/log/auth.log (perintah yang dijalankan).



