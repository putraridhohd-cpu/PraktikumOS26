# Praktikum 9.3C — Password Aging Policy
Tujuan: menerapkan kebijakan umur password dan mengamati efeknya.

## set aging policy untuk userA dan paksa userA ganti password saat login pertama
<img width="518" height="141" alt="image" src="https://github.com/user-attachments/assets/f101ff21-65ec-4fe8-b93f-35bce7c164a3" />

## kunci password userB lalu unlock kembali
<img width="335" height="131" alt="image" src="https://github.com/user-attachments/assets/7a1f6dfe-10d4-4e54-b9f6-b288b537fbcd" />

## Pertanyaan:
### 1. Apa arti nilai yang ditampilkan chage -l userA?
Nilai yang ditampilkan itu merincikan secara lengkap mengenai kebijakan masa berlaku password seperti kapan terakhir diganti,tanggal kedaluwarsa,sampai durasi peringatan sebelum password itu wajib diubah user.
<img width="1882" height="253" alt="image" src="https://github.com/user-attachments/assets/4a3583e5-0ca1-4a82-81e0-5643d42c2bb2" />

### 2. Bagaimana cara membuktikan userB terkunci dari output passwd -S?
Dengan melihat kode status satu huruf setelah nama pengguna pada baris output.
<img width="326" height="60" alt="image" src="https://github.com/user-attachments/assets/38ef199f-ea10-48ee-b77a-34c4aec83bbf" />
di gambar ada huruf L artinya locked,itu berarti userB sudah terbukti kalau sudah di lock!

### 3. Kapan sebaiknya menggunakan chage -d 0 vs passwd -e?
Keduanya punya fungsi yang sama buat memaksa user mengganti password saat login pertama kali,tapi chage -d 0 lebih spesifik karena memanipulasi data umur password secara langsung di sistem.
