# Praktikum 10.5 Script Monitor Memori

## buat script nano monitor-memori.sh
pindah ke directory praktikum-os/week10-memory (kalau belum buat,buat dulu dengan mkdir),lalu buat script nano monitor-memori.sh dengan isi:
<img width="1144" height="780" alt="image" src="https://github.com/user-attachments/assets/91abb288-1737-4538-a741-8393452664a9" />

## jalankan script monitor:
beri izin dengan chmod,lalu jalankan dengan bash:
<img width="1883" height="546" alt="image" src="https://github.com/user-attachments/assets/e4878e68-9943-47fa-bd16-4c258890fb88" />

## Analisis
### 1. Variabel THRESHOLD=20 menetapkan batas persentase. Perintah free | awk ’/Mem/ {printf "%d", $7/$2*100}’ mengambil kolom ke-7 (available) dibagikolom ke-2 (total) dari baris Mem, lalu dikalikan 100 untuk menghasilkan persentase bilangan bulat
Variabel THRESHOLD=20 berfungsi sebagai batas kritis, di mana perintah awk tersebut secara otomatis menghitung bahwa memori tersedia saat ini adalah 82% (hasil dari 1.6Gi/1.9Gi dikali 100).

### 2. Kondisi if [ "$AVAIL" -lt "$THRESHOLD" ] bernilai benar jika persentase memori tersedia di bawah 20.
Karena nilai AVAIL (82) jauh lebih besar daripada THRESHOLD (20), maka kondisi if itu bernilai salah sehingga script menjalankan perintah di bagian else dan menampilkan pesan bahwa status memori kamu masih dalam kategori normal.

## 3. Ubah THRESHOLD menjadi 90 dan jalankan ulang. Apa yang berubah pada output? Mengapa demikian?
<img width="1894" height="553" alt="image" src="https://github.com/user-attachments/assets/5f5a53e1-46a0-4e46-be91-cece363b9f76" />

setelah saya mengubah treshold nya jadi 90%,saya dapat peringatan "memori hanya tersedia 82%",
karena nilai memori yang tersedia saat ini yaitu 82 nilainya lebih kecil daripada ambang batas baru yang saya tetapkan (90), sehingga kondisi if [ "$AVAIL" -lt "$THRESHOLD" ] menjadi bernilai true dan memicu script untuk menjalankan perintah echo peringatan.


