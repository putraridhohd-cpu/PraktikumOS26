# Praktikum 10.4 Monitoring Memory

## output 
### output nya dan hasil dari mengurutkan berdasarkan memori
<img width="1914" height="768" alt="b8961623-1833-4b3e-afd2-c597b2087a17" src="https://github.com/user-attachments/assets/9d1bc4da-b5b3-401e-a02d-8671ed977775" />

### urutkan berdasarkan CPU
<img width="1307" height="321" alt="119bc2c4-35d5-46d1-9f1d-fae684b338e3" src="https://github.com/user-attachments/assets/fabb1b74-9011-4c65-9bc9-af06aa99a230" />

## Analisis
### 1. Proses apa yang berada di urutan pertama? Catat nilai %MEM dan RSS-nya.
Proses yang berada di urutan pertama adalah fwupd dengan nilai %MEM sebesar 2.1% dan RSS sebesar 43940 KB.

### 2. Konversikan RSS dari KB ke MB (bagi 1024). Misalnya, RSS=524288 berarti proses menggunakan 512 MB RAM. Apakah wajar untuk jenis program tersebut?
Nilai RSS itu setara dengan sekitar 42.9 MB (43940/1024),angka ini masih wajar buat layanan firmware update (fwupd) yang sedang berjalan di latar belakang pada sistem Linux.

### 3. Mengapa VSZ selalu lebih besar dari RSS pada proses yang sama?
VSZ (Virtual Memory Size) selalu lebih besar dari RSS (Resident Set Size) karena VSZ nampung seluruh memori yang dialokasikan proses termasuk shared libraries dan data di swap, kalau RSS cuman menghitung RAM yang sedang digunakan saat itu.

### 4. Apakah urutan proses di ps konsisten dengan tampilan top saat diurutkan berdasarkan %MEM?
Urutan proses pada ps dan top dalam output itu tidak terlihat sepenuhnya konsisten karena adanya perbedaan waktu pengambilan data (snapshot vs real-time) serta perbedaan algoritma pembulatan nilai memori yang ditampilkan oleh kedua tool itu.
