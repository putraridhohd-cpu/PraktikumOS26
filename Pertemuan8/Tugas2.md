# Tugas 2 Script Health Check Sistem
Sesuai instruksi pada Tugas 2 Script Health Check Sistem,saya akan menggabungkan konsep keamanan Bash (set -euo pipefail), penanganan interupsi (trap), dan pemantauan sistem.

## 1. Buat file healthcheck.sh nya
sesuai intruksi,kita buat dulu file nya:
```
nano ~/praktikum-os/week09/scripts/healthcheck.sh
```

## 2. isi file healthcheck.sh nya:
```
#!/bin/bash
# Tugas 2: Script Health Check Sistem (Professional Template)

# Konsep Wajib: set -euo pipefail
set -euo pipefail

# Inisialisasi Variabel
THRESHOLD=80
LOG_DIR="$HOME/praktikum-os/week09/logs"
LOG_FILE="$LOG_DIR/healthcheck-$(date '+%Y-%m-%d').log"

# Pastikan folder logs tersedia
mkdir -p "$LOG_DIR"

# Konsep Wajib: trap (Pembersihan saat exit atau interupsi)
cleanup() {
    echo -e "\n[INFO] Pemeriksaan dihentikan atau selesai."
}
trap cleanup EXIT

# Fungsi dengan variabel local
check_cpu() {
    local load=$(top -bn1 | grep "Cpu(s)" | awk '{print $2 + $4}')
    echo "Penggunaan CPU    : $load%"
}

check_memory() {
    local mem=$(free -m | awk 'NR==2{printf "%.2f%%", $3*100/$2 }')
    echo "Penggunaan Memori : $mem"
}

check_disk() {
    echo "Pemeriksaan Disk:"
    # Menggunakan for loop untuk setiap filesystem
    df -h --output=source,pcent,target | tail -n +2 | while read -r line; do
        local usage=$(echo "$line" | awk '{print $2}' | sed 's/%//')
        local mount=$(echo "$line" | awk '{print $3}')
        
        echo "  - $line"
        
        # Peringatan jika melebihi batas (Konsep if)
        if [ "$usage" -gt "$THRESHOLD" ]; then
            echo "    [PERINGATAN] Penggunaan disk di $mount melebihi batas ($THRESHOLD%)!"
        fi
    done
}

# Konsep Wajib: getopts untuk mengubah threshold
while getopts "t:" opt; do
    case $opt in
        t) THRESHOLD=$OPTARG ;;
        *) echo "Penggunaan: $0 [-t persen]"; exit 1 ;;
    esac
done

# Fungsi Utama yang akan ditampilkan ke terminal dan log menggunakan tee
run_healthcheck() {
    echo "=========================================="
    echo "SYSTEM HEALTH CHECK - $(date '+%Y-%m-%d %H:%M:%S')"
    echo "=========================================="
    echo "Hostname          : $(hostname)"
    echo "Uptime            : $(uptime -p)"
    check_cpu
    check_memory
    echo "------------------------------------------"
    check_disk
    echo "=========================================="
}

# Konsep Wajib: tee (Simpan ke log dan tampilkan sekaligus)
run_healthcheck | tee -a "$LOG_FILE"
```
<img width="1199" height="1022" alt="Screenshot 2026-05-02 081939" src="https://github.com/user-attachments/assets/559c408b-e4bc-4d33-9cff-5639eba8e136" />
Simpan dengan CTRL+O lalu keluaar dengan CTRL+X 

## 3. Beri izin untuk eksekusi nya:
```
chmod +x ~/praktikum-os/week09/scripts/healthcheck.sh
cd ~/praktikum-os/week09/scripts/
```

## 4. Jalankan dengan threshold default (80%):
```
./healthcheck.sh
```
### HASILNYA:
<img width="1587" height="641" alt="image" src="https://github.com/user-attachments/assets/60faabd3-bc79-4e1a-88cf-f501b2e4c365" />

Pada gambar, script berhasil menampilkan kondisi kesehatan sistem secara menyeluruh mulai dari uptime hingga penggunaan disk tanpa memicu peringatan karena semua partisi masih di bawah batas 80%.


## 5. Jalankan dengan opsi -t (misal set ke 10% agar peringatan muncul):
```
./healthcheck.sh -t 10
```
### HASILNYA:
<img width="1130" height="609" alt="image" src="https://github.com/user-attachments/assets/1bdd44f1-19b2-45a1-9b01-5199b1d66eac" />
Berdasarkan Gambar, script berhasil memberi peringatan visual otomatis pada partisi root karena penggunaan disk sebesar 51% telah melampaui batas sensitivitas 10% yang dimasukkan melalui parameter getopts

## 6. Pengecekan file log healthcheck.log dengan cat
```
cat ../logs/healthcheck-$(date '+%Y-%m-%d').log
```
### HASILNYA:
<img width="1402" height="960" alt="image" src="https://github.com/user-attachments/assets/25e5ca9e-2109-4eb4-a8ca-51fcbed24e45" />
Eksekusi perintah cat pada gambar membuktikan bahwa seluruh hasil pengecekan sistem telah tersalin dengan sempurna ke dalam file log secara permanen berkat penggunaan perintah tee
