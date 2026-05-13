# Praktek 10.1: Amati Layanan Aktif Saat Boot
Periksa layanan yang berjalan di sistem dan identifikasi layanan yang paling lambat saat boot.

## 1. Lihat semua layanan yang sedang berjalan.
<img width="776" height="395" alt="image" src="https://github.com/user-attachments/assets/c2c7c70d-4f49-4be8-bdf7-e91c72361d78" />
Sistem ada 18 layanan yang aktif, termasuk layanan krusial seperti ssh.service buat akses remote dan cron.service untuk penjadwalan tugas. Seluruh unit itu berstatus loaded dan active,yang berarti konfigurasi berhasil dimuat dan layanan berfungsi normal.

## 2. Lihat semua unit service yang ada (aktif maupun tidak)
<img width="589" height="469" alt="image" src="https://github.com/user-attachments/assets/88a968e9-e736-4bf9-955f-6ba0c4049be9" />

Daftar menunjukkan berbagai status unit seperti apparmor.service berstatus enabled,terus beberapa lainnya berstatus static artinya layanan itu hanya berjalan kalau dipanggil oleh layanan lain, bukan berjalan sendiri secara mandiri.

## 3. Analisis waktu boot dan temukan layanan paling lambat.
<img width="521" height="308" alt="image" src="https://github.com/user-attachments/assets/266b8188-1161-4177-8c53-4e9fd65fb08d" />

Waktu yang dibutuhkan sistem buat sampai ke graphical target adalah 17.915 detik, dengan kontribusi terbesar dari kernel selama 11.146 detik. Layanan snapd.seeded.service dan snapd.service jadi penyumbang waktu boot terlama (masing2 di atas 3 detik), sehingga bisa menjadi fokus optimasi jika ingin mempercepat proses startup.

## TANTANGAN
Identifikasi tiga layanan dengan waktu inisialisasi terlama menggunakan systemd-analyze blame. Gunakan pipeline dari Bab 3 (| sort -rh | head -3) untuk mempercepat pencariannya. Untuk setiap layanan, cari tahu fungsinya dengan systemctl cat nama-layanan. Tuliskan nama layanan, waktu inisialisasinya, dan penjelasan singkat fungsinya

### 1. snapd.seeded.service
* Waktu Inisialisasi: 3.191 detik.
* Fungsi: Layanan ini bertanggung jawab untuk melakukan inisialisasi awal (seeding) pada paket-paket Snap yang sudah terpasang secara pre-installed di sistem agar siap digunakan oleh pengguna.

### 2. snapd.service
* Waktu Inisialisasi: 3.062 detik.
* Fungsi: Ini adalah layanan utama (daemon) untuk pengelolaan paket Snap; fungsinya mencakup manajemen siklus hidup aplikasi Snap, termasuk pemasangan, pembaruan, dan pengoperasian kontainer aplikasi tersebut.

### 3. systemd-networkd-wait-online.service
* Waktu Inisialisasi: 1.279 detik.
* Fungsi: Layanan ini bertugas untuk menunda proses boot lebih lanjut sampai koneksi jaringan benar-benar terkonfigurasi dan "online", memastikan layanan yang bergantung pada internet tidak gagal saat dijalankan.
