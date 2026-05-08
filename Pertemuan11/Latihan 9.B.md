# Latihan 9.B — Kebijakan Akun dan Quota
Tugas: Tuliskan langkah untuk membuat user intern, menambahkannya ke group labgroup, memaksa pergantian password tiap 45 hari (warning 7 hari), memberi izin sudo hanya untuk systemctl status, dan
menetapkan quota ruang serta inode sederhana pada /home/.


## Langkah 1: Manajemen User dan Group
Membuat entitas baru untuk lingkungan kerja terbatas:
<img width="374" height="63" alt="image" src="https://github.com/user-attachments/assets/406e24e4-ace1-497b-919f-20ee5eb021ae" />
sudah terlihat ya user nya sudah berhasil dimasukkin ke group tanpa error

## Langkah 2: Pengaturan Kebijakan Password
Mengatur siklus hidup password biar lebih aman:
<img width="548" height="149" alt="image" src="https://github.com/user-attachments/assets/d143b6eb-c574-47ac-8732-47c754be292c" />

## Langkah 3: Pemberian Hak Akses Sudo Terbatas
Mengizinkan user menjalankan perintah spesifik tanpa memberikan akses admin penuh,ketik:
```
sudo visudo -f /etc/sudoers.d/lab-intern
```
lalu isi:
<img width="644" height="128" alt="Screenshot 2026-05-08 095256" src="https://github.com/user-attachments/assets/15d7af1b-5ffc-44e4-8273-1f4e2eb03746" />

## Langkah 4: Buat disk virtual kecil untuk simulasi home intern:
ketik:
```
sudo dd if=/dev/zero of=/tmp/home-intern.img bs=1M count=50
sudo mkfs.ext4 /tmp/home-intern.img
```
<img width="643" height="206" alt="image" src="https://github.com/user-attachments/assets/95555530-a2f9-4809-be91-ae733d41d0dc" />

## langkah 5: Mount dengan opsi quota aktif
ketik:
```
sudo mkdir -p /mnt/home-intern
sudo mount -o loop,usrquota /tmp/home-intern.img /mnt/home-intern
```

## langkah 6: Inisialisasi database quota di disk itu
ketik:
```
sudo quotacheck -cum /mnt/home-intern
sudo quotaon -v /mnt/home-intern
```
<img width="930" height="85" alt="image" src="https://github.com/user-attachments/assets/555e5268-1228-4afd-9090-c5acc2ca2029" />

## langkah 7: Menetapkan Quota Sederhana pada /home/
ketik:
```
sudo edquota -u intern
```
lalu ubah soft nya jadi 10240 dan hard nya 20480
<img width="768" height="114" alt="image" src="https://github.com/user-attachments/assets/869a2bdd-0c42-466c-af62-35bca008c29f" />

## Langkah 7: kita beri file pancingan agar user intern tercatat di sistem quota,lalu eksekusi:
```
sudo touch /mnt/home-intern/test-intern
sudo chown intern:intern /mnt/home-intern/test-intern
```
lalu eksekusi dengan:
```
sudo repquota /mnt/home-intern
```
<img width="596" height="161" alt="image" src="https://github.com/user-attachments/assets/dd26cc28-d004-462f-a496-da4c28d215cd" />

Tabel repquota paling bawah menunjukkan kalau user intern sudah diubah nilainya jadi 10240 di kolom soft dan 20480 di kolom hard. Baris ini muncul setelah kita memancing sistem dengan perintah touch

kalo gak di pancing hasilnya malah kayak gini:
<img width="589" height="139" alt="image" src="https://github.com/user-attachments/assets/27e857f2-f95d-46f1-bedb-2b0b73e5d61e" />


## Kesimpulan:
Seluruh konfigurasi keamanan pada Latihan 9.B sudah dibuat. Sistem sekarang punya kontrol yang ketat terhadap user intern, mulai dari pembatasan waktu password, pembatasan perintah administratif, hingga pengendalian kapasitas penyimpanan data agar tidak membebani server.

