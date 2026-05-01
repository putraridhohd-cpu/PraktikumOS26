# Praktikum 7.3: Script Grading & Menu Interaktif

## 1. Buat script grading (menggunakan if dan for): 
```
nano ~/praktikum-os/week09/scripts/grading-batch.sh
```

## 2. lalu isi scripts Grading-batch.sh nya:
<img width="1228" height="813" alt="image" src="https://github.com/user-attachments/assets/11ed03f3-0a78-469a-a6b9-00bbe9d811e5" />

## 3. Simpan,beri izin,dan jalankan: 
```
chmod +x ~/praktikum-os/week09/scripts/grading-batch.sh
~/praktikum-os/week09/scripts/grading-batch.sh
```

### Hasilnya:
<img width="1535" height="345" alt="image" src="https://github.com/user-attachments/assets/e05d96cf-adac-4a7f-80bf-7524466418c9" />

## 4. Buat script menu interaktif (while + case):
```
nano ~/praktikum-os/week09/scripts/menu-sistem.sh
```

## 5. lalu isi Script menu-sistem.sh nya:
<img width="1282" height="652" alt="image" src="https://github.com/user-attachments/assets/38bf2fd1-064b-461b-b49e-9b8edfe25991" />

## 6. Beri izin dan jalankan, coba setiap opsi:
<img width="1005" height="1018" alt="image" src="https://github.com/user-attachments/assets/bc803011-9441-46ce-aea9-0f57e2a3c115" />



# Latihan 9.3: Ringkasan Jumlah Grade
Tugasnya adalah memodifikasi grading-batch.sh agar di bagian bawah muncul ringkasan berapa orang yang dapat A, B, C, D, dan E menggunakan perulangan for kedua.

## 1. modifikasi file grading-batch.sh
buka kembali file nya dengan:
```
nano grading-batch.sh
```
lalu modifikasi seperti ini:
<img width="1234" height="1012" alt="image" src="https://github.com/user-attachments/assets/be8ad1c3-f5a0-4a9a-b14e-46d4ac0086a9" />

simpan lalu keluar

## 2. lalu beri izin dan jalankan:
<img width="871" height="372" alt="Screenshot 2026-05-01 173854" src="https://github.com/user-attachments/assets/4fff8bc3-1184-4dd4-8fe1-47090926b202" />

saya menggunakan dua perulangan for. Perulangan pertama berfungsi untuk menampilkan detail nilai tiap mahasiswa. Perulangan kedua (bagian ringkasan) digunakan untuk mencocokkan setiap kriteria grade dengan isi array. Dengan cara ini, script menjadi lebih informatif karena tidak hanya menampilkan data mentah, tapi juga hasil pengolahan statistiknya secara otomatis.

