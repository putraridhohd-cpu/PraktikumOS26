# Latihan 10.3 Investigasi Log dan Keamanan SSH
di latihan ini,saya akan analisis log sistem dan tingkatkan keamanan konfigurasi SSH.

## Langkah 1: Investigasi Log Error
perintah ini untuk mencari error sejak boot terakhir dan menghitung jumlahnya:
<img width="473" height="48" alt="image" src="https://github.com/user-attachments/assets/98cc1931-ea25-436f-b9f8-eb73100ff856" />


Filter log nya sudah berhasil mengidentifikasi 8 baris pesan error (kotak merah) sejak waktu booting terakhir. ini berarti sistem masih stabil karena jumlah error yang terekam masih sedikit untuk sebuah sesi operasional server.

## Langkah 2: Meningkatkan Keamanan SSH
Ikuti alur aman (backup -> edit -> validasi -> reload).
<img width="940" height="194" alt="image" src="https://github.com/user-attachments/assets/78ddf554-7691-4974-8e09-6d070a143a97" />

penjelasan:
* PermitRootLogin no: Menutup celah bagi pengguna root untuk login langsung via SSH, memaksa penggunaan user biasa demi keamanan.
* MaxAuthTries 3: Membatasi percobaan login hingga 3 kali untuk mencegah serangan brute-force.
* LoginGraceTime 30: Mempercepat waktu pemutusan koneksi jika pengguna tidak segera login dalam 30 detik.

## Langkah 3: Verifikasi Perubahan
<img width="685" height="423" alt="image" src="https://github.com/user-attachments/assets/cb51e3f6-92ed-41ef-ba33-2df0aa03a448" />

di output layanan ssh.service tetap berjalan secara active (kotak hijau) setelah perubahan diterapkan. Verifikasi menggunakan grep mengonfirmasi bahwa parameter baru telah terbaca dengan benar oleh sistem. Penggunaan port 22 juga terlihat masih mendengarkan (listening) secara normal pada alamat IPv4(kotak merah) dan IPv6(kotak kuning).

## Langkah 4: Kembalikan Konfigurasi (Restore)
Setelah selesai melihat hasilnya dan memastikannya bekerja, kembalikan ke kondisi semula agar kita tidak terkunci dari akses root di kemudian hari jika diperlukan:
<img width="543" height="78" alt="image" src="https://github.com/user-attachments/assets/70fbf9ab-b38b-43a6-8f3a-08a9daceaf0d" />

Langkah terakhir untuk mengembalikan file (kotak merah) dengan berkas backup sudah berhasil. Ini adalah praktik standar dalam administrasi sistem untuk memastikan server kembali ke kondisi stabil setelah melakukan pengujian keamanan.
