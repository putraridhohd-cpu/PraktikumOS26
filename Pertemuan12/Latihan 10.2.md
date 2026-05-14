# Latihan 10.2 Layanan Kustom dengan Restart Otomatis
disini saya akan membuat layanan systemd kustom yang mendemonstrasikan fitur restart otomatis.

## Langkah 1: Buat Skrip Bash monitor-disk.sh
Jalankan perintah ini untuk membuat skrip di direktori home nya:
<img width="485" height="137" alt="image" src="https://github.com/user-attachments/assets/b905b655-42ea-4323-9420-4a59946ebcac" />

lalu berikan izin eksekusi pada skrip nya:
```
chmod +x ~/monitor-disk.sh
```
nah disini Skrip berhasil dibuat dengan loop while true yang menjalankan perintah df -h dan date setiap 30 detik. Output lalu diarahkan ke file ~/disk-usage.log. Izin eksekusi (chmod +x) telah diberikan sehingga skrip siap dijalankan oleh sistem.

## Langkah 2: Buat Berkas Unit Service
Kita akan membuat file service di /etc/systemd/system/.
<img width="704" height="227" alt="image" src="https://github.com/user-attachments/assets/ed9c66c9-00bb-42e5-9681-4c9d7840bf29" />

disini saya sudah daftarin berkas unit ke dalam /etc/systemd/system/. Parameter Restart=always dan RestartSec=5s sangat penting dalam latihan ini karena sistem akan selalu mengecek apakah proses sudah mati dan akan mengaktifkan kembali setelah jeda selama 5 detik.

## Langkah 3: Aktifkan dan Jalankan Layanan
Jalankan 2 perintah ini untuk memuat ulang daemon dan menjalankan layanan baru:
<img width="935" height="258" alt="image" src="https://github.com/user-attachments/assets/c726d4f8-6672-418f-8006-012177430c46" />

Layanan berhasil dimuat ulang (kotak merah), diaktifkan (kotak kuning), dan dijalankan (kotak orange). Status menunjukkan active (kotak hjau),beratti tandanya konfigurasi User=ridho26 dan jalur ExecStart sudah tepat.

## Langkah 4: Simulasi Crash
Untuk menguji fitur Restart=always, kita akan mematikan prosesnya secara paksa:
<img width="847" height="299" alt="image" src="https://github.com/user-attachments/assets/e55b9a6f-2f52-4761-a2c3-e3eae01f040a" />

Saat proses dengan PID 1304 (kotak biru) dibunuh secara paksa menggunakan kill -9, unit service mendeteksi kegagalan itu (di kotak merah). Sesuai instruksi konfigurasi, systemd melakukan scheduled restart. terbukti dari status akhir yang menunjukkan layanan kembali active dengan Main PID 1321 (kotak hijau), membuktikan fitur daya tahan layanan bekerja dengan baik.

## Langkah Terakhir: Pembersihan (Cleanup)
<img width="538" height="117" alt="image" src="https://github.com/user-attachments/assets/fd8b5f8e-bf76-4610-8f43-a8ec543a7c63" />

