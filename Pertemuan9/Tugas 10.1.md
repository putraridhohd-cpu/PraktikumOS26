# Tugas Praktikum 10.1 Audit Penggunaan Memori Sistem
Instruksi: Buat script memory-audit.sh yang menghasilkan laporan kondisi memori sistem secara otomatis

## 1. Buat script memory-audit.sh dan isi file nano dengan ini:
<img width="1140" height="563" alt="image" src="https://github.com/user-attachments/assets/a478417c-2672-44de-91ce-944cfef5f719" />

## 2. Jalankan script audit
<img width="1463" height="943" alt="image" src="https://github.com/user-attachments/assets/63fce446-6662-4379-89c7-651572523395" />

## Analisis
### 1. Hitung persentase memori tersedia (available / total × 100%). Apakah sistem dalam kondisi normal?
Persentase memori tersedia adalah sekitar 84% (1.6Gi/1.9Gi * 100%),jadi sistem masih normal karena ketersediaan memori masih jauh di atas ambang batas kritis (umumnya 20%)
<img width="604" height="70" alt="image" src="https://github.com/user-attachments/assets/780734df-28d9-4fe3-9a54-9508fde5099f" />

### 2. Mengapa buff/cache tidak dihitung sebagai memori yang terpakai dari sudut pandang ketersediaan untuk aplikasi?
karena kernel bisa mengosongkan/melepas isi cache itu secara instan kapan pun aplikasi membutuhkan RAM tambahan.

### 3. Dari /proc/meminfo, apakah SwapTotal lebih besar dari 0? Berapa nilai SwapFree?
dari data /proc/meminfo, swapTotal bernilai 2097148 kB (lebih besar dari 0) dan nilai SwapFree juga sama,berati ruang swap tersedia penuh dan tidak sedang digunakan sama sekali.
<img width="222" height="254" alt="image" src="https://github.com/user-attachments/assets/20baaea6-50a9-4b79-8cc7-f04467dfe0d5" />

