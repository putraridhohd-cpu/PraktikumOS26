# Praktek 10.4: Filter dan Analisis Log Layanan

# 1. Kode 1.22: Log SSH satu jam terakhir
<img width="699" height="127" alt="image" src="https://github.com/user-attachments/assets/4e5fe5aa-62df-4a02-b438-cec2067311f5" />

ini adalah riwayat SSH setelah sistem melakukan reboot. Terlihat log "Server listening on 0.0.0.0 port 22" yang menandakan layanan siap menerima koneksi.

## 2. Kode 1.23: Log prioritas error dari boot saat ini
<img width="944" height="98" alt="image" src="https://github.com/user-attachments/assets/52d4b559-c6bc-49bf-bba1-2d6b9eb15c84" />

Sistem mendeteksi beberapa peringatan terkait vmwgfx (driver grafis di virtual machine) dan snapd. Meskipun berwarna merah, ini umum terjadi di lingkungan virtual dan tidak menghentikan fungsi utama sistem.

## 3. Kode 1.24: Pantau log SSH secara real-time
### Terminal pertama:
<img width="1404" height="258" alt="image" src="https://github.com/user-attachments/assets/4caf7332-5268-4bf0-abe4-a1880411f123" />

terminal pertama langsung mencatat aktivitas tersebut secara real-time:
* Accepted password for ridho26 from 127.0.0.1 port 57286 ssh2.
* Ini membuktikan mekanisme pemantauan log -f (follow) berfungsi dengan baik.
### Terminal kedua (untuk memicu aktivitas):
<img width="550" height="490" alt="image" src="https://github.com/user-attachments/assets/24767bc5-c20f-4550-843c-7e5427a417f9" />

## 4. Ekstrak log ke berkas untuk analisis
<img width="699" height="77" alt="image" src="https://github.com/user-attachments/assets/af04b2bc-276f-4cbb-b2ec-662992659876" />
saya dapat 21 baris log SSH untuk hari ini, dan juga Perintah grep tidak menampilkan baris apa pun (kosong), yang berarti layanan SSH nya sudah berjalan sangat bersih hari ini tanpa ada kegagalan login atau error sistem.
