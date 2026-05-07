# Tugas 10.3 Membuat dan Memverifikasi Swap File
Instruksi: Buat swap file khusus tugas sebesar 256 MB dan verifikasi.

## 1. Buat dan aktifkan swap file tugas
<img width="1404" height="200" alt="image" src="https://github.com/user-attachments/assets/f1b7e074-db13-471a-9f6b-84f553d68192" />

## 2. Verifikasi dan simpan hasil
<img width="600" height="230" alt="image" src="https://github.com/user-attachments/assets/7a251e55-465e-4dc5-84de-283fc04030d1" />

## Analisis
### 1. Identifikasi kolom NAME, TYPE, SIZE, dan USED pada output swapon –show.
Berdasarkan kolom pada swapon --show:
* NAME: Nama jalur file swap, yaitu /swap.img dan /swapfile-tugas-week10.
* TYPE: Jenis swap yang digunakan,di output keduanya adalah file.
* SIZE: Kapasitas swap, yaitu 2G untuk swap utama dan 256M untuk swap tugas.
* USED: Jumlah memori swap yang sedang terpakai, di mana keduanya bernilai 0B (belum terpakai).
<img width="319" height="69" alt="image" src="https://github.com/user-attachments/assets/bbb512d2-727c-4fe5-995a-9f460cfd4eb4" />

### 2. Apakah nilai total pada baris Swap di free -h bertambah 256 MB?
Ya, nilai total pada baris Swap di free -h bertambah jadi 2.2Gi. Awalnya sistem nya punya swap sebesar 2.0Gi,setelah ditambah swap file tugas 256MB totalnya jadi meningkat
<img width="367" height="68" alt="image" src="https://github.com/user-attachments/assets/44e510f4-ecce-4af9-9124-b7e29c2ce7ac" />

### 3. Mengapa permission 600 penting? Apa risiko jika diatur ke 644?
Permission 600 penting karena file swap berisi data mentah dari RAM yang mungkin memuat informasi sensitif seperti password.kalau diatur ke 644, pengguna lain di dalam sistem bisa membaca isi file nya,jadi beresiko data pribadi atau keamanan sistem jadi bocor
