# Praktikum 10.2 Mengamati Aktivitas Paging

## Langkah 1: Jalankan vmstat dengan interval 1 detik, 5 sampel
jalankan:
```
vmstat 1 5
```
<img width="1216" height="257" alt="504a0b0f-6cd5-45d2-bf85-dfd66e405d3a" src="https://github.com/user-attachments/assets/ee0ad8b3-a0dc-45eb-994c-9bf51f91d7fb" />


## Analisis:
### 1. Amati nilai si dan so pada kelima baris. Pada sistem normal dengan RAM cukup, kedua nilai ini selalu 0.
Nilai si dan so di kelima baris nya masih bernilai 0,itu artinya sistem nya masih bekerja dengan normal
<img width="156" height="228" alt="image" src="https://github.com/user-attachments/assets/e61215bb-22f9-4b6d-94ea-f1ce899c16e8" />

### 2. Jika nilai si atau so sesekali muncul lebih dari 0, artinya pernah ada aktivitas swap. Ini masih wajar jika tidak terus-menerus.
seperti gambar di no 1,belum ada nilai si/so yang lebih dari 0,berarti sistem tidak pernah melakukan aktivitas swap

### 3. Jika si dan so terus-menerus lebih dari 0, sistem dalam kondisi memory pressure serius — performa turun drastis karena akses disk jauh lebih lambat dari RAM.
seperti di gambar no 1,si dan so masih stabil di angka 0

## 4. Perhatikan juga kolom free (RAM kosong) dan buff (buffer) untuk memahami kondisi keseluruhan RAM saat itu.
kondisi RAM maasih longgar karena nilai free stabil di angka 1344588 dan nilai buff di sekitar 19572,jadi kapasitas memori fisik masih tersedia luas buat jalanin proses lainnya
<img width="200" height="109" alt="image" src="https://github.com/user-attachments/assets/1d27bd1f-477e-41d8-9d92-578786e6c58f" />
