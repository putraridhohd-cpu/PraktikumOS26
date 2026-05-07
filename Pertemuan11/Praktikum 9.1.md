# Praktikum 9.1 — Permissions
Tujuan: membaca permission, mengubahnya dengan aman, dan memahami efek chmod, chown, serta umask pada file nyata.

## Langkah 1: Buat direktori kerja dan dua file uji.
<img width="508" height="145" alt="image" src="https://github.com/user-attachments/assets/49e13ac0-9e7d-49f7-be0c-6583cf233161" />

## Langkah 2: Jadikan secret.txt privat hanya untuk owner.
<img width="432" height="47" alt="image" src="https://github.com/user-attachments/assets/582fa6e2-e0f2-45b1-9794-86f58999822e" />

## langkah 3 : Jadikan myscript.sh dapat dijalankan.
<img width="437" height="71" alt="image" src="https://github.com/user-attachments/assets/fbbb7b73-ec6d-402d-8271-583c97669cbf" />

## Langkah 4: Buat direktori bersama dan amati efek SGID sederhana.
<img width="828" height="118" alt="image" src="https://github.com/user-attachments/assets/5ec56352-f020-499b-adfb-773bfd4aaa5e" />

## Langkah 5: Uji efek umask pada file baru.
<img width="801" height="208" alt="image" src="https://github.com/user-attachments/assets/0cc7ed0b-4a8c-4acf-9ceb-3f63ebbd5a3f" />

## Analisis
### 1. Mengapa secret.txt tidak dapat dibaca oleh group dan others setelah chmod 600?
Perintah chmod 600 sudah mencabut semua hak akses baca, tulis, dan eksekusi bagi group dan others sehingga file itu jadi privat dan hanya bisa diakses oleh owner nya aja

### 2. Apa perbedaan arti 600 dan 755 terhadap file yang diuji?
Permission 600 memberi akses baca tulis terbatas hanya untuk pemilik tanpa hak eksekusi,kalau 755 memberikan hak penuh kepada pemilik dan mengizinkan orang lain untuk melihat dan eksekusi file itu sebagai program

### 3. Setelah umask 027, permission apa yang dihasilkan untuk file baru, dan mengapa bukan 777?
Permission yang dihasilkan adalah 640 karena nilai umask 027 memotong hak tulis bagi group dan seluruh akses bagi others dari nilai dasar default sistem untuk sebuah file baru.
