# Praktikum 10.6 Mengamati System Call dengan strace
Tujuan: melihat dan menganalisis system call yang dilakukan suatu perintah

## Langkah 1: Lihat 30 baris pertama system call dari perintah ls
<img width="1671" height="877" alt="9801cf5f-b06c-467c-a27b-8e2c7e3cd16d" src="https://github.com/user-attachments/assets/d15abbde-21a6-4cd6-a33c-6cb591524000" />

## Langkah 2: Lihat ringkasan statistik dan bandingkan dua direktori berbeda.
<img width="1125" height="912" alt="7ae76523-bfe1-42b1-bddb-9aa68ab5c96b" src="https://github.com/user-attachments/assets/7718e47d-6bf7-4705-be92-35dfd357e423" />


## Analisis
### 1. Dari output Langkah 1, identifikasi minimal 4 system call berbeda. Jelaskan fungsi singkat masing-masing berdasarkan argumen yang terlihat.
* execve: Menjalankan program /usr/bin/ls dengan argumen dan variabel lingkungan tertentu.
* openat: Membuka file atau direktori (seperti /etc/ld.so.cache atau library sistem) buat dibaca.
* mmap: Memetakan file atau memori ke dalam ruang alamat proses, biasanya dipakai untuk memuat shared libraries.
* fstat: Mengambil informasi statistik tentang file (seperti ukuran file atau izin akses) berdasarkan deskriptor file yang terbuka.
<img width="840" height="435" alt="image" src="https://github.com/user-attachments/assets/058ffce6-9c63-4fd8-8fd2-aa7056f189d8" />

### 2. Dari ringkasan strace -c, system call mana yang paling sering dipanggil? Mengapa?
System call yang paling sering dipanggil adalah mmap (sebanyak 18 kali). karena setiap kali program butuh library pendukung atau alokasi memori baru buat memproses data, sistem perlu memetakan memori itu berulang kali biar bisa dipakai program ls.
<img width="555" height="103" alt="image" src="https://github.com/user-attachments/assets/22e72e6b-3483-44ce-ad13-f438e8f12c9d" />

### 3. Apakah ada system call dengan errors lebih dari 0? Apakah itu berarti program bermasalah, ataukah bagian normal dari logika program?
ada,di statfs ada 2 error dan acces ada 2 error,kalau menurut logika program sih ini normal karena program sering mencoba memeriksa keberadaan file konfigurasi atau library di beberapa lokasi berbeda kalau tidak ditemukan di lokasi pertama (error), program otomatis mencari di lokasi berikutnya.
<img width="1072" height="739" alt="image" src="https://github.com/user-attachments/assets/1b2e7269-4200-41ac-b9d2-e94df2fc2ff4" />

### 4. Apakah jumlah system call berbeda antara ls dan ls /etc? Faktor apa yang menyebabkan perbedaan tersebut?
iya beda,di gambar ada 74 panggilan,itu karena objek yang dihapus,kalau jalanin ls /etc mengharuskan kernelbuat melakukan banyak operasi buat buka direktori /etc,membaca entri didalam nya banyak banget dan mengambil atribut file dari setiap item yang ada di folder itu dibandingkan hanya menjalankan ls di folder kosong atau folder biasa.
