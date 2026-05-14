# Praktek 10.3: Buat Layanan Sederhana dari Skrip Bash
Buat layanan systemd yang menjalankan server HTTP sederhana berbasis Python.

## 1. Kode 1.13: Menyiapkan direktori dan konten layanan
```
cd ~/lab-os/chapter10-services
mkdir -p situs-demo
nano situs-demo/index.html
```
isi berkas index.html:
<img width="1212" height="370" alt="image" src="https://github.com/user-attachments/assets/c0f30be4-a9e4-4cc4-963b-9f19f7b38396" />

## 2. Kode 1.14: Skrip server HTTP untuk layanan
```
nano ~/lab-os/chapter10-services/jalankan-server.sh
```
Isi berkas jalankan-server.sh:
<img width="1480" height="301" alt="image" src="https://github.com/user-attachments/assets/32565910-d00d-450e-a6e6-41251a5c656a" />

beri izin eksekusi:
```
chmod +x ~/lab-os/chapter10-services/jalankan-server.sh
```

## 3. Kode 1.15: Membuat berkas unit kustom
```
nano ~/lab-os/chapter10-services/demo-web.service
```
Isi berkas demo-web.service:
(Catatan: Ganti nama-pengguna-kamu menjadi ridho26)
<img width="1417" height="466" alt="image" src="https://github.com/user-attachments/assets/9569a593-7e6b-42f9-b61e-ba2765d5a8b9" />

Salin dan muat ulang systemd:
```
sudo cp ~/lab-os/chapter10-services/demo-web.service /etc/systemd/system/demo-web.service
sudo systemctl daemon-reload
```

## 4. Kode 1.16: Menjalankan dan memverifikasi layanan kustom
<img width="650" height="197" alt="image" src="https://github.com/user-attachments/assets/22c8b385-3c44-4804-b23e-78b56bbd869e" />

## 5. Kode 1.17: Menguji restart otomatis
<img width="1186" height="505" alt="image" src="https://github.com/user-attachments/assets/b7aedb46-778d-4c1c-b1d3-0a59797a9877" />

Ketika proses dihentikan paksa menggunakan kill -9, systemd mendeteksi kegagalan tersebut dengan status result 'signal'. Sesuai dengan konfigurasi Restart=on-failure, sistem otomatis memicu Scheduled restart dan menghidupkan kembali layanan dengan PID baru (1228) hanya dalam hitungan detik

## 6. Bersihkan layanan uji setelah selesai
```
sudo systemctl disable --now demo-web
sudo rm /etc/systemd/system/demo-web.service
sudo systemctl daemon-reload
```

## TANTANGAN
<img width="883" height="244" alt="image" src="https://github.com/user-attachments/assets/fc868f10-d77c-4268-98d3-e2444ecb50bf" />

### 1. Modifikasi Berkas Unit
Buka kembali berkas unit kustom nya:
```
nano ~/lab-os/chapter10-services/demo-web.service
```
Ubah isinya menjadi seperti ini
<img width="1375" height="546" alt="image" src="https://github.com/user-attachments/assets/ff5492df-99c1-4c02-a64e-2cea4c9b4e88" />

### 2. Terapkan Perubahan
Jalankan urutan perintah berikut untuk memperbarui sistem:
<img width="908" height="80" alt="image" src="https://github.com/user-attachments/assets/0494ffb8-e09c-46f8-a128-f0d5413589e5" />

### 3. Uji Layanan
<img width="766" height="280" alt="image" src="https://github.com/user-attachments/assets/d7be5eed-e7df-44d0-ac7d-b42505a9384c" />

* Verifikasi Port Baru: Output curl menunjukkan bahwa server sekarang merespons pada port 9091, membuktikan bahwa penggunaan variabel Environment="PORT=9091" dan variabel $PORT pada ExecStart telah terkonfigurasi dengan benar.
* Status Persistence: Layanan kini berstatus enabled, yang ditandai dengan pembuatan symlink ke multi-user.target.wants. Ini memastikan layanan web kustom kamu akan langsung berjalan otomatis setiap kali server Ubuntu kamu dinyalakan.
* Konfirmasi Modifikasi: Log status menampilkan deskripsi baru yaitu "Demo Web Server Praktek Bab 10 (Modifikasi)", yang mengonfirmasi bahwa systemd telah berhasil membaca ulang berkas unit yang telah kamu perbarui menggunakan daemon-reload.
