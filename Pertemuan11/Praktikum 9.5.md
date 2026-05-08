# Praktikum 9.5 — Disk Quota
Tujuan: memahami alur quota secara aman pada loopback filesystem tanpa mengubah filesystem utama.

## Langkah 1: Buat image filesystem kecil dan mount dengan opsi quota.
<img width="610" height="218" alt="image" src="https://github.com/user-attachments/assets/b8ed5a55-1bb0-454e-becf-8e0c3fbcd3ef" />

## Langkah 2: Buat database quota dan aktifkan enforcement.
<img width="947" height="233" alt="image" src="https://github.com/user-attachments/assets/d60e8ac8-6681-4413-b90c-d75ef1eb19e4" />

## Langkah 3: Tetapkan quota untuk user uji dan amati hasilnya.
ketik:
```
sudo edquota -u userA
# contoh: soft block 5120, hard block 10240
sudo repquota /mnt/quota-test
```
dan didalamnya ubah soft jadi 5120 dan hard jadi 10240
<img width="713" height="139" alt="image" src="https://github.com/user-attachments/assets/0dd3704f-1d94-4fbc-a18a-3a9b60a7dfe1" />

## Analisis
### 1. Apa perbedaan soft limit dan hard limit saat quota mulai terlampaui?
Soft limit berfungsi sebagai batas peringatan nya user bisa nambah data selama masa tenggang (grace period), sedangkan hard limit adalah batas mutlak yang sama sekali tidak bisa dilewati; jika tercapai, sistem akan langsung menolak proses tulis data.

### 2. Mengapa praktikum ini memakai loopback filesystem, bukan langsung /home/?
Terlihat dari penggunaan perangkat /dev/loop4 pada setiap baris perintah dan output. Ini menunjukkan bahwa kuota hanya bekerja pada file image virtual, bukan pada hardisk fisik /home
<img width="519" height="156" alt="image" src="https://github.com/user-attachments/assets/c2882d6e-25c7-48cc-aa8e-010b81e39c14" />

### 3. Dari output repquota, informasi apa yang menunjukkan quota sudah aktif?
<img width="534" height="153" alt="image" src="https://github.com/user-attachments/assets/59f6e7e3-1b41-40e4-a619-9f88431a97e4" />
* Munculnya baris Block grace time: 7days; Inode grace time: 7days yang menunjukkan sistem sudah siap menghitung masa tenggang jika soft limit terlampaui.

<img width="941" height="204" alt="image" src="https://github.com/user-attachments/assets/1034ea46-8ecc-4cbb-94e6-9f88c65642c1" />
* Status yang dikotaki yang muncul sebelum tabel laporan.
