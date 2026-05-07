# Tugas 10.2 Identifikasi Proses dengan Memori Tertinggi
Instruksi: Simpan daftar 10 proses pengguna memori terbesar ke file.

## 1. Simpan dan tampilkan proses teratas
<img width="1876" height="408" alt="image" src="https://github.com/user-attachments/assets/06352129-8e87-4339-92ee-da8eb8884955" />

## Analisis
### 1. Proses apa di urutan pertama? Catat nilai %MEM dan RSS.
Proses yang berada di urutan pertama adalah /usr/libexec/fwupd/fwupd dengan nilai %MEM sebesar 2.1% dan RSS sebesar 44000 KB
<img width="937" height="98" alt="image" src="https://github.com/user-attachments/assets/7dd7d8c9-ab60-4dcb-9622-0cb751ccf80c" />

### 2. Konversikan RSS ke MB (bagi 1024). Apakah wajar?
nilai RSS itu 44000 dibagi 1024 = 42,97 MB,itu masih wajar untuk sebuah layanan pembaruan firmware sistem yang berjalan di latar belakang.

## 3. Jumlahkan %MEM dari 5 proses teratas. Berapa persen RAM yang mereka gunakan bersama?
Jumlah %MEM dari 5 proses teratas adalah 7.2% (hasil penjumlahan dari 2.1+1.9+1.3+1.1+0.8), berarti kelima proses itu secara bersama-sama memakai kurang dari 1/10 total kapasitas RAM sistem.
<img width="327" height="169" alt="image" src="https://github.com/user-attachments/assets/ca499ce8-6b83-489b-9e4c-32293f930a8a" />

