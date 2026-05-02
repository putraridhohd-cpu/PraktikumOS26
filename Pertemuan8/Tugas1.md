# Tugas 1 Script Absensi Kelas

## 1. buat file absensi.sh 
sesuai instruksi nya,saya akan memmbuat script absensi.sh di scripts/
```
nano ~/praktikum-os/week09/scripts/absensi.sh
```

## 2. isi file nya
isi file absensi.sh nya dengan kode berikut:
```
#!/bin/bash
# Tugas 1: Script Absensi Kelas

# Path folder dan file
LOG_DIR="$HOME/praktikum-os/week09/logs"
TANGGAL=$(date '+%Y-%m-%d')
LOG_FILE="$LOG_DIR/absensi-$TANGGAL.txt"

# Pastikan folder logs ada
mkdir -p "$LOG_DIR"

# Fungsi Bantuan
tampilkan_bantuan() {
    echo "Penggunaan: $0 [opsi] <nama_mahasiswa> <status>"
    echo "Status: hadir, izin, alpha"
    echo ""
    echo "Opsi:"
    echo "  -r    Tampilkan rekapitulasi jumlah per status"
    echo "  -h    Tampilkan bantuan ini"
}

# Fungsi Rekapitulasi
tampilkan_rekap() {
    if [ ! -f "$LOG_FILE" ]; then
        echo "Belum ada data absensi untuk hari ini ($TANGGAL)."
        return
    fi
    echo "=== Rekapitulasi Absensi $TANGGAL ==="
    for s in hadir izin alpha; do
        JUMLAH=$(grep -c " - $s" "$LOG_FILE" || echo 0)
        echo "$s: $JUMLAH"
    done
}

# Handle Opsi menggunakan getopts
while getopts "rh" OPSI; do
    case $OPSI in
        r) tampilkan_rekap; exit 0 ;;
        h) tampilkan_bantuan; exit 0 ;;
        *) tampilkan_bantuan; exit 1 ;;
    esac
done

# Shift untuk mengambil parameter posisinal setelah opsi
shift $((OPTIND - 1))

# Ambil Argumen Nama dan Status
NAMA=$1
STATUS=$2

# Validasi input wajib
if [ -z "$NAMA" ] || [ -z "$STATUS" ]; then
    echo "ERROR: Nama dan status harus diisi!"
    tampilkan_bantuan
    exit 1
fi

# Validasi status yang diperbolehkan
if [[ ! "$STATUS" =~ ^(hadir|izin|alpha)$ ]]; then
    echo "ERROR: Status harus 'hadir', 'izin', atau 'alpha'."
    exit 1
fi

# Simpan entri ke file (Redirection)
WAKTU=$(date '+%H:%M')
echo "[$WAKTU] $NAMA - $STATUS" >> "$LOG_FILE"
echo "Berhasil mencatat: $NAMA ($STATUS)"
```
<img width="1040" height="984" alt="Screenshot 2026-05-02 075211" src="https://github.com/user-attachments/assets/29ea4f85-da6f-4896-a307-e9e19fe4d467" />
simpan dengan CTRL+O dan keluar dengan CTRL+X

## 3. beri izin eksekusi:
```
chmod +x ~/praktikum-os/week09/scripts/absensi.sh
cd ~/praktikum-os/week09/scripts/
```

## 4. Input 5 data mahasiswa (contoh):
```
./absensi.sh "Ridho" hadir
./absensi.sh "Budi" hadir
./absensi.sh "Ani" izin
./absensi.sh "Siti" hadir
./absensi.sh "Eko" alpha
```
### HASILNYA:
<img width="1265" height="284" alt="image" src="https://github.com/user-attachments/assets/8479b88f-5e8b-4b3b-a5a0-5fb6cb395de8" />
itu berarti saya sudah berhasil membuat 2 poin yang di instruksi tugas praktikum yaitu membuat script yang "Menerima argumen nama mahasiswa dan status (hadir/izin/alpha)"

## 5. Tampilkan Rekapitulasi:
```
./absensi.sh -r
```
### HASILNYA:
<img width="840" height="125" alt="image" src="https://github.com/user-attachments/assets/bf066b41-8580-48b6-9159-833eb4eabfc3" />
itu berarti saya sudah berhasil membuat poin 3 yang di instruski yaitu membuat "Opsi -r: tampilkan rekapitulasi (jumlah per status)"

## 6. cek isi file log-nya:
```
cat ../logs/absensi-$(date '+%Y-%m-%d').txt
```

### HASILNYA:
<img width="1145" height="185" alt="image" src="https://github.com/user-attachments/assets/52ecc9d8-b450-4032-9508-afd52f8ee86d" />
itu berarti saya sudah berhasil membuat poin ke 2 yang di intruksi yaitu "Menyimpan entri ke absensi-YYYY-MM-DD.txt dengan format [HH:MM]
NAMA - STATUS"

## 7. tampilkan bantuan dengan opsi -h:
```
./absensi.sh -h
```
### HASILNYA:
<img width="870" height="200" alt="image" src="https://github.com/user-attachments/assets/2b28cdab-0877-48cb-bd78-8e4ac3c32cae" />
