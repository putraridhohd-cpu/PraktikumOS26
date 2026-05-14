# Latihan 10.1 Audit Layanan dan Analisis Boot
<img width="765" height="230" alt="image" src="https://github.com/user-attachments/assets/3198d2a3-1dc0-41a4-a5d5-750204da3c0d" />

## Langkah 1: Audit Layanan Berjalan
<img width="652" height="380" alt="image" src="https://github.com/user-attachments/assets/88a2d093-53d9-4248-b34a-16db5f1af168" />

yang saya kotaki adalah 3 layanan yang saya kenal,mari kita cek statusnya satu persatu dengan perintah:
```
systemctl status <nama-layanan>
```

### 1. ssh.service(kotak kuning)
<img width="821" height="274" alt="image" src="https://github.com/user-attachments/assets/8efe98b2-c6b4-4fb1-8be2-09a8645daa4c" />

Berjalan normal, berfungsi menyediakan akses remote secure shell.

### 2. cron.service (kotak merah):
<img width="896" height="212" alt="image" src="https://github.com/user-attachments/assets/ab8e8cbe-baca-4ce1-9ac8-d23e389a8995" />

Berjalan normal, berfungsi untuk menjalankan tugas penjadwalan otomatis (background jobs).

### 3. systemd-journald.service (kotak hijau):
<img width="892" height="389" alt="image" src="https://github.com/user-attachments/assets/fa1664ac-dc17-430a-b6dc-afb002cc46af" />

Berjalan normal, berfungsi sebagai pengelola pengumpulan data log sistem.

## Langkah 2: Analisis Waktu Booting
lalu kita lihat 5 layanan dengan waktu inisialisasi terlama:
<img width="416" height="80" alt="image" src="https://github.com/user-attachments/assets/52459b49-8c43-450a-8358-6d70b9869564" />

disini ada 5 layanan dengan waktu inisialisasi terlama,layanan snapd.seeded.service dan snapd.service di posisi teratas.tapi total waktu boot ini masih  wajar untuk lingkungan server virtual.

## Langkah 3: Identifikasi Layanan Gagal
<img width="280" height="55" alt="image" src="https://github.com/user-attachments/assets/ec416d3f-5f23-42e2-803e-733acfce6854" />

hasil nya menunjukan menunjukkan angka 0,berarti seluruh unit layanan pada Ubuntu Server berhasil dimuat dan dijalankan tanpa ada error

## Kesimpulan:
Sistem Ubuntu Server berada dalam kondisi optimal, semua layanan inti berfungsi dengan baik, dan tidak ditemukan adanya service failure.
