# Studi Kasus 10.2 Gagal Akses File
Skenario: Program tidak dapat membaca file konfigurasi. Penyebab umum: file tidak ada, path salah, atau permission tidak sesuai. Kita akan mensimulasikan kondisi ini dan mengamati pesan error yang dihasilkan.

## Langkah 1: Buat direktori dan file konfigurasi contoh.
<img width="1449" height="245" alt="image" src="https://github.com/user-attachments/assets/5ba73dfc-edcf-4631-bf2d-4dffffc331c1" />

## Langkah 2: Simulasikan permission bermasalah.
<img width="1183" height="132" alt="image" src="https://github.com/user-attachments/assets/f7ac1851-544a-45f0-b442-cac12b5b98df" />

## Langkah 3: Kembalikan permission dan verifikasi.
<img width="1186" height="130" alt="image" src="https://github.com/user-attachments/assets/d791fed5-a83e-4513-bc4e-1146f644e73c" />

## Analisis
### 1. Mengapa cat menghasilkan Permission denied setelah chmod 000? System call apa yang gagal?
Perintah cat menghasilkan Permission denied karena bit izin baca sudah dihapus semua, jadinya system call openat() gagal dieksekusi oleh kernel karena user tidak memiliki hak akses untuk membuka file itu.

### 2. Apa perbedaan pesan error Permission denied vs No such file or directory? Coba rm app.conf lalu cat app.conf untuk melihat perbedaannya
<img width="1084" height="131" alt="image" src="https://github.com/user-attachments/assets/f5f20b47-4828-47bf-9c72-4ecf34b5ec9d" />
di gambar itu,eksekusi perintah cat app.conf setelah rm app.conf menghasilkan pesan error karena file tersebut memang sudah tidak ada lagi di dalam sistem penyimpanan, yang secara mendasar membedakannya dengan error "Permission denied" di mana file tersebut sebenarnya masih ada tetapi kernel menolak akses untuk membukanya karena tidak adanya izin baca.

### 3. Permission 644 berarti apa untuk owner, group, dan others?
Permission 644 berarti owner memiliki akses penuh untuk membaca dan menulis (rw-),kalau group dan others hanya diberikan izin untuk membaca saja (r--) tanpa bisa mengubah isi file tersebut.

