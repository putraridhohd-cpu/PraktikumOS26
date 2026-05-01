# Praktikum 7.6 Debugging Script

## 1.  Buat script untuk dianalisis:
```
nano ~/ praktikum -os/ week09 / scripts /debug - latihan .sh
```

## 2. isi file nya:
<img width="1213" height="737" alt="image" src="https://github.com/user-attachments/assets/d0d6dfba-f30b-40b7-a6c1-fa7647d785da" />

simpan file nya lalu keluar

## 3. beri izin lalu eksekusi:
<img width="1144" height="946" alt="image" src="https://github.com/user-attachments/assets/dcf7524a-280f-4393-919f-7a298ae28f46" />


# Latihan 9.5: Perbaikan Debugging
Menggunakan teknik debugging untuk menganalisis script dan menambahkan mekanisme pencegahan error (error handling) agar script tidak berhenti secara tidak wajar saat menemui kondisi yang tidak terduga.

## 1. Modifikasi isi file debug_latihan nya
Saya menambahkan dua fitur utama sesuai instruksi:
* set -e: Untuk memastikan script langsung berhenti jika ada perintah yang gagal.
* Pengecekan Eksistensi Direktori: Menambahkan validasi -d untuk memastikan direktori tujuan benar-benar ada sebelum perintah du dijalankan.
<img width="1265" height="570" alt="image" src="https://github.com/user-attachments/assets/3f85d282-c8b4-4b80-8810-d6081b720251" />

## 2. beri izin dan eksekusi file nya:
<img width="1166" height="135" alt="image" src="https://github.com/user-attachments/assets/5bc78972-2922-4a9b-8f9d-eeef69275044" />

Berdasarkan pengujian pada terminal:
* Perintah ./debug-latihan.sh /folder/ngasal 100 dijalankan.
* Script tidak lagi menampilkan error sistem dari perintah du, melainkan menampilkan pesan error kustom: "ERROR: Direktori '/folder/ngasal' tidak ditemukan atau bukan folder!".

## analisis
Tanpa adanya pengecekan -d, script akan tetap mencoba menjalankan perintah du pada folder yang tidak ada, yang akan menghasilkan pesan error standar Linux yang kurang rapi. Dengan menambahkan validasi ini, script menjadi lebih robust (tangguh) dan mudah dipahami oleh pengguna jika terjadi kesalahan input.
