# Praktikum 10.3 Membuat dan Mengonfigurasi Swap File
di sini kita langsung aja ke output dan analisis nya:

## Output
<img width="1161" height="659" alt="image" src="https://github.com/user-attachments/assets/0f89d255-8028-49a7-8dcc-bb62b76a721c" />

## Analisis:
### 1. Berapa nilai swappiness default? Apa artinya bagi perilaku kernel dalam menggunakan swap?
Nilai nya adalah 60,berarti kernel bakalan mulai mindahin data dari RAM ke swap secara moderat ketika penggunaan memori fisik sudah mencapai sekitar 40%.
<img width="456" height="181" alt="image" src="https://github.com/user-attachments/assets/0b0e7e71-cd4e-47cb-9d9a-86b334560ab1" />

### 2. Setelah diubah ke 10, konfirmasi nilai berubah pada output cat kedua. Apa dampak nilai 10 terhadap penggunaan swap dibanding nilai 60?
nilai itu sudah dikonfirmasi berubah jadi 10 di cat kedua,dampak nilai rendah ini adalah kernel akan memprioritaskan penggunaan RAM fisik lalu akan menggunakan swap jika kondisi memori benar2 sudah sangat kritis.
<img width="389" height="91" alt="image" src="https://github.com/user-attachments/assets/f8861168-856d-470e-88f2-99db971898f4" />

### 3. Apakah entri /swapfile-week10 muncul di swapon –show? Jika tidak, pastikan Langkah 2 (chmod 600) sudah dijalankan sebelum Langkah 3
Entri nya sudah muncul di output swapon --show dengan ukuran 512M
<img width="326" height="94" alt="image" src="https://github.com/user-attachments/assets/6767ebf2-295e-4d85-84a6-e7bf22529845" />

itu berarti langkah pembuatan, pemberian izin akses (chmod 600), sampai pengaktifan swap file baru sudah berhasil dijalankan semua.
