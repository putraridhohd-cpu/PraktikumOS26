# Tugas 10.5 Studi Kasus Diagnosa Server Lambat
Skenario: Server terasa lambat. Buat script diagnosa yang menggabungkan semua
pemeriksaan dari bab ini menggunakan fungsi Bash.

## 1. Buat file diagnosa
buat file diagnosa dengan nano diagnosa-server.sh lalu isi di dalam nya dengan kode ini:
```
#!/bin/bash
set -euo pipefail

LAPORAN="diagnosa-server-lambat.txt"
WARN_MEM=false
WARN_SWAP=0

cek_memori() {
    echo "--- Kondisi Memori ---"
    free -h
    echo
    AVAIL_PCT=$(free | awk '/Mem/ {printf "%d", $7/$2*100}')
    if [ "$AVAIL_PCT" -lt 20 ]; then
        echo "PERINGATAN: Memori tersedia hanya ${AVAIL_PCT}%"
        WARN_MEM=true
    fi
}

cek_swap() {
    echo "--- Penggunaan Swap ---"
    swapon --show 2>/dev/null || echo "Tidak ada swap aktif"
    echo
    WARN_SWAP=$(free | awk '/Swap/ {print $3}')
    if [ "$WARN_SWAP" -gt 0 ]; then
        echo "INFO: Swap digunakan (${WARN_SWAP} kB)"
    fi
}

cek_proses() {
    echo "--- 10 Proses Memori Tertinggi ---"
    ps aux --sort=-%mem | head -n 11
    echo
}

cek_paging() {
    echo "--- Aktivitas Paging (5 sampel) ---"
    vmstat 1 5
    echo
}

ringkasan() {
    echo "=== RINGKASAN ==="
    if [ "$WARN_MEM" = true ]; then
        echo "- Memori: KRITIS - perlu tindakan segera"
    else
        echo "- Memori: normal"
    fi

    if [ "$WARN_SWAP" -gt 0 ]; then
        echo "- Swap: aktif - pantau aktivitas paging"
    else
        echo "- Swap: tidak digunakan"
    fi
}

{
    echo "=== LAPORAN DIAGNOSA SERVER ==="
    date
    echo

    cek_memori
    cek_swap
    cek_proses
    cek_paging
    ringkasan
} | tee "$LAPORAN"

echo
echo "Laporan disimpan ke: $LAPORAN"
```

## 2. jalankan dan lihat hasilnya:
<img width="2048" height="2260" alt="image" src="https://github.com/user-attachments/assets/7a763dd4-7537-4bb5-a70b-044ac8a74cec" />

## Analisis
### 1. Jelaskan peran masing-masing fungsi: cek_memori, cek_swap, cek_proses,cek_paging, dan ringkasan. Mengapa diagnosa dipecah menjadi fungsi terpisah?
* cek_memori: Menampilkan statistik RAM dan menghitung persentase ketersediaan untuk mendeteksi kekurangan memori.
* cek_swap: Memeriksa apakah ada memori cadangan (swap) yang sedang digunakan oleh sistem.
* cek_proses: Mengidentifikasi 10 aplikasi atau proses yang mengonsumsi RAM paling besar.
* cek_paging: Memantau aktivitas keluar-masuk data antara RAM dan disk dalam rentang waktu tertentu.
* ringkasan: Memberikan kesimpulan akhir mengenai status kesehatan memori sistem secara cepat.
* Alasan dipecah: Diagnosa dipecah menjadi fungsi agar kode lebih rapi, mudah dikelola, dan memungkinkan pemanggilan modul tertentu secara spesifik tanpa harus menjalankan seluruh isi script.
<img width="1916" height="1005" alt="Screenshot 2026-05-07 135541" src="https://github.com/user-attachments/assets/86c33491-5463-4e12-9c1d-958928c1fab7" />

 ### 2. Berdasarkan bagian RINGKASAN, apakah kondisi sistem normal atau kritis? Jelaskan berdasarkan nilai threshold yang digunakan script.
 kondisi sistem masih normal,karena nilai memori tersedia pada output menunjukkan angka 84% (1.6Gi/1.9Gi),jadi nilai ini jauh lebih besar daripada threshold (ambang batas) 20% yang ditetapkan di dalam script.

 ### 3. Mengapa script menggunakan tee "$LAPORAN" bukan redirection biasa > "$LAPORAN"? Apa keuntungannya?
agar output dari diagnosa itu bisa ditampilkan di layar terminal sekaligus disimpan ke dalam file laporan secara bersamaan. kalau cuman menggunakan redirection biasa (>), output akan langsung masuk ke file tanpa muncul di terminal,jadinya pengguna tidak bisa melihat hasilnya secara real-time.

### 4. Dari output cek_paging, apakah ada aktivitas si atau so? Jika ada, apa implikasinya terhadap performa server?
Pada output cek_paging (bagian swap), kolom si dan so nya bernilai 0. Implikasinya adalah performa server saat ini sangat optimal karena sistem tidak perlu melakukan pertukaran data antara RAM dan disk, yang berarti kapasitas RAM fisik masih mencukupi untuk menangani semua proses yang berjalan.
<img width="613" height="128" alt="image" src="https://github.com/user-attachments/assets/1ddd9941-190e-45a8-8a7c-7c33c66be287" />

