# Tugas 10.4 Analisis System Call dengan strace
Instruksi: Analisis system call yang dipanggil perintah ls.

## 1. Simpan ringkasan dan detail system call
<img width="1800" height="1060" alt="image" src="https://github.com/user-attachments/assets/370b526c-dbaf-4ca1-8a4d-dcaedaaa4e01" />
<img width="1009" height="741" alt="image" src="https://github.com/user-attachments/assets/8f0a35a6-575f-44d2-aa6b-1a576d10517c" />

## Analisis
### 1.  Sebutkan minimal 5 system call dari strace-summary.txt beserta fungsi singkatnya.
* openat: Membuka file atau direktori untuk dibaca atau ditulis.
* mmap: Memetakan file atau perangkat ke dalam memori (biasanya dipakai buat memuat shared libraries).
* fstat: Mengambil status atau informasi statistik dari sebuah file (seperti ukuran atau izin).
* close: Menutup deskriptor file yang sudah tidak digunakan lagi agar sumber daya dilepaskan.
* read: Membaca data dari deskriptor file yang sedang terbuka.
<img width="479" height="117" alt="image" src="https://github.com/user-attachments/assets/ad4b6db5-8fe0-4b95-ad67-c7ad5d04b409" />

### 2. System call mana yang paling sering dipanggil? Mengapa?
System yang paling sering di call adalah mmap (sebanyak 18 kali).karena setiap kali perintah ls dijalankan, sistem perlu memetakan berbagai pustaka standar (libraries) dan mengalokasikan ruang memori yang cukup biar program bisa berjalan
<img width="265" height="113" alt="image" src="https://github.com/user-attachments/assets/81b65259-d9fb-4571-b54a-8efd149c47e9" />

### 3. Apakah ada errors lebih dari 0? Apakah program tetap berjalan normal meskipun ada kegagalan tersebut?
Ya, ada 2 errors lebih dari 0,yaitu acces (2 error) dan statfs (2 error).tapi program tetap berjalan normal karena error nya biasanya terjadi saat sistem mencoba mencari file konfigurasi atau library di lokasi tertentu yang memang tidak ada, lalu secara otomatis sistem akan langsung mencari di lokasi alternatif lainnya hingga ketemu.
<img width="269" height="174" alt="image" src="https://github.com/user-attachments/assets/76ae6b60-1d99-491f-8fe7-afcd53258f3f" />
