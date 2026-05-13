# Praktek 10.2: Kelola Layanan SSH
Praktikkan semua operasi dasar systemctl pada layanan SSH yang tersedia di sistem.

## 1. Analisis Status SSH (Kode 1.8)
<img width="818" height="331" alt="image" src="https://github.com/user-attachments/assets/19e5cf3f-c6bb-4fcb-8b3f-6b42c9e9f3a9" />

* Status Aktif(kotak merah): Layanan SSH terpantau active (running)
* Aksesibilitas(kotak putih): Output is-active menghasilkan jawaban active, namun is-enabled menunjukkan status disabled. Ini berarti SSH sedang berjalan sekarang, tetapi tidak akan otomatis aktif saat komputer dinyalakan ulang (reboot).
* Log Koneksi(kotak kuning): Pada bagian bawah log status pertama, terlihat ada koneksi yang berhasil diterima (Accepted password) dari IP 192.168.75.100.

## 2. Analisis Restart Layanan (Kode 1.9)
<img width="1210" height="550" alt="image" src="https://github.com/user-attachments/assets/47663567-0371-4c3d-b40a-11f0dc5444ff" />

* Perubahan PID(kotak merah): Setelah menjalankan sudo systemctl restart ssh, Main PID berubah dari 1049 jadi 1296. Perubahan angka PID ini adalah indikator utama bahwa proses lama telah dihentikan dan proses baru telah berhasil dijalankan.
* Waktu Aktif(kotak hijau): Baris Active: active (running) menunjukkan durasi baru yaitu 27ms ago, mengonfirmasi bahwa layanan baru saja dimulai ulang.

## 3. Analisis Dependensi SSH (Kode 1.10)
Output ini menampilkan daftar panjang layanan yang harus siap agar SSH bisa berfungsi
<img width="389" height="458" alt="image" src="https://github.com/user-attachments/assets/90b82209-d6a0-4d97-8007-693f3dd2147b" />

ini adalah dependensi yang penting:
* system.slice(kotak putih): Untuk manajemen sumber daya.
* sysinit.target(kotak merah): Layanan dasar inisialisasi sistem.
* systemd-journald.service(kotak hijau): Untuk pencatatan log aktivitas SSH.
* apparmor.service(kotak kuning): Untuk keamanan pembatasan akses program.

## 4. Cek semua unit yang gagal di sistem
<img width="290" height="72" alt="image" src="https://github.com/user-attachments/assets/f92e70aa-590f-4f9d-bb5a-647612552f6e" />

perintah ini menunjukkan 0 loaded units listed. Ini adalah kabar baik karena artinya tidak ada layanan yang gagal berjalan pada sistem kamu saat ini.

## TANTANGAN:
Buat skrip Bash (referensi Bab 7) bernama cek-layanan.sh yang memeriksa status daftar layanan dari sebuah berkas teks. Berkas teks daftar-layanan.txt berisi satu nama layanan per baris (isi minimal: ssh, cron, rsyslog). Skrip membaca setiap nama layanan, memeriksa statusnya dengan systemctl is-active, lalu menulis laporan ke berkas laporan-layanan.log dengan format: [TANGGAL] nama-layanan: ACTIVE/INACTIVE. Gunakan date untuk mendapatkan tanggal.

### 1. Buat Berkas Daftar Layanan
Pertama, buat berkas teks input sesuai instruksi:
```
nano daftar-layanan.txt
```
isi:

<img width="584" height="68" alt="image" src="https://github.com/user-attachments/assets/62dccd80-dbc8-477c-b30e-6f5c2693d5f9" />


### 2. Buat Skrip Bash (cek-layanan.sh)
<img width="581" height="418" alt="image" src="https://github.com/user-attachments/assets/386eefe2-fcea-4f7c-a3a8-4a52dc702d21" />

## 3. cek isi laporan nya:
<img width="423" height="147" alt="image" src="https://github.com/user-attachments/assets/eec50502-fd9e-4635-b02a-5be6073b09ca" />

* Layanan Utama (kotak merah): Ketiga layanan inti ini terpantau dalam status ACTIVE pada kedua waktu pengecekan (04:05:42 dan 04:07:16). Hal ini menunjukkan bahwa layanan remote access, penjadwalan tugas, dan sistem log berjalan dengan stabil tanpa gangguan.
* Baris Kosong/Invalid(kotak kuning): ada satu entri : INACTIVE pada log pertama yang disebabkan oleh adanya baris kosong atau karakter tersembunyi di akhir berkas daftar-layanan.txt. Masalah ini sudah berhasil diatasi setelah kamu melakukan pembersihan karakter menggunakan perintah sed, sehingga log kedua (04:07:16) sudah bersih dan akurat.
