# Praktikum 10.1 Melihat Penggunaan Memori

## Langkah 1: Jalankan free -h untuk melihat ringkasan RAM dan swap
jalankan:
```
free -h
```
<img width="1173" height="119" alt="image" src="https://github.com/user-attachments/assets/ff2b061b-4f1b-472d-bc3e-3f750e6a91d2" />

## Langkah 2: Lihat detail memori dari kernel melalui /proc/meminfo.
jalankan:
```
cat /proc/meminfo | head -n 20
```
<img width="827" height="635" alt="image" src="https://github.com/user-attachments/assets/d2826727-b4c8-45b9-a8c5-68e88e6760b2" />

## Analisis
### 1. Hitung persentase memori tersedia: available / total × 100%. Jika hasilnya di bawah 10%, sistem mulai kekurangan memori
kalau dari output yanhg ada di gambar, persentase memori tersedia masih aman di angka sekitar 84,2% (1.6Gi / 1.9Gi)
<img width="1160" height="60" alt="image" src="https://github.com/user-attachments/assets/c1328df4-ae44-4681-a158-1e770a8e147c" />


### 2. Pada baris Swap, apakah kolom used bernilai 0? Jika lebih dari 0, kernel sudah pernah memindahkan data ke disk karena RAM tidak cukup
kolom used pada Swap bernilai 0B yang menandakan kernel belum perlu menggunakan disk karena RAM masih mencukupi
<img width="244" height="61" alt="image" src="https://github.com/user-attachments/assets/80a83b21-8160-4652-9e11-332bc4192626" />

### 3. Perhatikan field Cached dan Buffers di /proc/meminfo. Nilai ini sesuai dengan kolom buff/cache pada free -h.
total nilai Buffers (18704 kB) dan Cached (399980 kB) di /proc/meminfo memang sinkron dengan kolom buff/cache (395Mi) pada perintah free -h.
<img width="497" height="148" alt="image" src="https://github.com/user-attachments/assets/b337d8a9-0e6d-4487-b9ec-cffd5aea8739" />

* Total: 18.704 + 399.980 = 418.684 kB
* Konversi ke Mi (Mebibyte):418.684/1024 = 408,8 MB
* 418.684/1024/1,024 = 0,399 Gi atau sekitar 399 MiB


