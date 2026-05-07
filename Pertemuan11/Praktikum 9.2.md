# Praktikum 9.2 — ACL
Tujuan: memahami ACL dari nol: melihat kondisi awal, menambah akses untuk satu user, lalu membuat direktori yang mewariskan ACL otomatis.

## Langkah 1: Siapkan file dan lihat permission standar tanpa ACL tambahan.
<img width="457" height="176" alt="image" src="https://github.com/user-attachments/assets/0e960148-2941-41a4-9e96-a236bad71016" />

## Langkah 2: Beri akses baca ke satu user tertentu tanpa mengubah owner atau group.
sebelum kita beri akses,kita buat dulu contoh user nya:
<img width="539" height="313" alt="image" src="https://github.com/user-attachments/assets/c97de50f-2074-4c10-83a5-a40359fa7e09" />
lalu kita tambahkan ACL untuk satu user itu:
<img width="1005" height="354" alt="image" src="https://github.com/user-attachments/assets/366f1fb9-f462-4884-9a8e-c37017680f5f" />

## Langkah 3: Buat direktori bersama yang mewariskan ACL ke file baru.
<img width="805" height="787" alt="image" src="https://github.com/user-attachments/assets/8cf34070-48f5-4b70-9849-7c94d7e9b959" />
disitu hanya userA saja yang kebagian karena userB nya belum saya buat

## Analisis
### 1. Mengapa getfacl confidential.txt awalnya tidak menampilkan user tertentu?
getfacl awalnya cuma nampilin entri standar karena file tersebut baru dibuat dan hanya memiliki permission dasar Linux tanpa ada aturan Access Control List tambahan yang spesifik untuk user atau group lain.

### 2. Setelah setfacl -m u:userA:r confidential.txt, apa perbedaan output ls -l dan getfacl?
Output ls -l sekarang nampilin tanda plus setelah permission yang menandakan adanya ACL aktif, sementara getfacl merincikan secara detail bahwa userA sekarang punya hak akses baca secara khusus pada file tersebut.

### 3. Mengapa file inherited.txt mewarisi ACL dari direktori shared?
karena pada direktori shared telah dipasang Default ACL menggunakan opsi -d, sehingga setiap file baru yang dibuat di dalamnya secara otomatis akan mewarisi aturan akses yang sama tanpa perlu diatur manual lagi.
