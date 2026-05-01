# Praktikum 7.5 Script Backup dengan Opsi

# 1. Buat script:
```
nano ~/ praktikum -os/ week09 / scripts /backup - data .sh
```

## 2. Ketik isi berikut:
```
#!/bin/bash
# Penggunaan: ./backup-data.sh [-v] [-c] [-l logfile] <sumber> <tujuan>

VERBOSE=false
COMPRESS=false
LOG_FILE=""

while getopts "vcl:" OPSI; do
    case $OPSI in
        v) VERBOSE=true ;;
        c) COMPRESS=true ;;
        l) LOG_FILE="$OPTARG" ;;
        *) echo "Penggunaan: $0 [-v] [-c] [-l logfile] <sumber> <tujuan>"
           exit 1 ;;
    esac
done

shift $((OPTIND - 1))
SUMBER=$1
TUJUAN=$2

log() {
    local MSG="[$(date '+%T')] $1"
    echo "$MSG"
    [ -n "$LOG_FILE" ] && echo "$MSG" >> "$LOG_FILE"
}

# Validasi input
[ -z "$SUMBER" ] || [ -z "$TUJUAN" ] && { echo "ERROR: sumber dan tujuan wajib diisi"; exit 1; }
[ ! -d "$SUMBER" ] && { log "ERROR: $SUMBER tidak ada"; exit 2; }

mkdir -p "$TUJUAN"
TANGGAL=$(date '+%F-%H%M%S')

[ "$VERBOSE" = true ] && log "Sumber: $SUMBER | Tujuan: $TUJUAN"

if [ "$COMPRESS" = true ]; then
    ARSIP="$TUJUAN/backup-$(basename "$SUMBER")-$TANGGAL.tar.gz"
    tar -czf "$ARSIP" -C "$(dirname "$SUMBER")" "$(basename "$SUMBER")"
    log "Arsip: $ARSIP ($(du -sh "$ARSIP" | cut -f1))"
else
    cp -r "$SUMBER" "$TUJUAN/backup-$(basename "$SUMBER")-$TANGGAL"
    log "Backup selesai."
fi
```

## 3. Beri izin dan uji:
<img width="1542" height="683" alt="image" src="https://github.com/user-attachments/assets/c4bce20f-aff1-4ac1-a688-52d8328af382" />
