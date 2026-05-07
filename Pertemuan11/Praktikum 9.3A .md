# Praktikum 9.3A — Membuat dan Mengelola User
Tujuan: membuat user baru, memodifikasi propertinya, dan memahami perbedaan opsi useradd dan usermod.

## 1. buat 2 user dulu
<img width="436" height="163" alt="image" src="https://github.com/user-attachments/assets/d4a8e128-ccbc-44c0-802a-29d611db9a45" />
karena di praktikum sebelumnya yaitu praktikum 9.2 (pertemuan 11) saya sudah membuat userA,saya hapus lagi dengan ``` sudo userdel -r userA ```

## 2. Verifikasi
<img width="365" height="76" alt="image" src="https://github.com/user-attachments/assets/3b860a59-d463-422f-afd3-c128230dd798" />

## 3. modifikasi shell userA
<img width="400" height="79" alt="image" src="https://github.com/user-attachments/assets/cdd4ee1c-3648-4e9d-8360-4b25ba8ece1e" />

## 4. lock dan unlock userB
<img width="327" height="104" alt="image" src="https://github.com/user-attachments/assets/6cce2050-cf30-4ed7-861d-4dc2ba070f92" />

## Pertanyaan
### 1. Apa perbedaan output id userA sebelum dan sesudah menambah group?
Perintah id userA awalnya cuman menampilkan group bawaan user itu,tapi setelah user dimasukkan ke grup baru, maka pada bagian groups akan muncul tambahan ID dan nama group yang menandakan hak aksesnya sudah bertambah.

### 2. Bagaimana status passwd -S userB berubah saat akun di-lock?
Status pada perintah passwd -S berubah dari huruf P (Password set) jadi L (Locked) yang artinya akun userB telah dikunci dan tidak bisa digunakan untuk login meskipun password yang dimasukkan benar.
<img width="400" height="106" alt="image" src="https://github.com/user-attachments/assets/220d1de3-d2d8-45d6-bfda-2285fca5fce8" />

