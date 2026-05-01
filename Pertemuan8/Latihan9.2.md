# Praktikum 7.2 Script Info Sistem dengan Argumen

## 1. buat script:
```
nano ~/praktikum-os/week09/scripts/info-sistem.sh
```

## 2. lalu isi script nya dengan kode ini:
<img width="1215" height="600" alt="image" src="https://github.com/user-attachments/assets/547b8f43-3007-4488-9000-a7e0c2462fe2" />

## 3. simpan,lalu beri izin dan uji dengan beberapa argumen:
```
cd ~/praktikum-os/week09/scripts/

./info-sistem.sh

./info-sistem.sh "Dian" 50

./info-sistem.sh "Dian" 10
```
### Hasilnya:
<img width="1257" height="680" alt="image" src="https://github.com/user-attachments/assets/d2676c8d-95e3-4f3e-9b37-6aca32be04df" />



# Latihan 9.2: Membuat Script Kalkulator Sederhana
## Tujuan:
Membuat script Bash yang mampu melakukan operasi matematika dasar (penjumlahan, pengurangan, perkalian, dan pembagian) menggunakan parameter posisional dan struktur kontrol case

## 1. buat dulu file nya
ketik:
```
nano ~/praktikum-os/week09/scripts/kalkulator.sh
```

## 2. isi file tersebut dengan kode program ini:
```
#!/bin/bash

# Validasi jumlah argumen
if [ $# -lt 3 ]; then
    echo "Error: Argumen tidak lengkap."
    echo "Penggunaan: $0 <angka1> <operator> <angka2>"
    exit 1
fi

ANGKA1=$1
OPERATOR=$2
ANGKA2=$3

# Pemilihan operasi menggunakan case
case $OPERATOR in
    +)
        HASIL=$((ANGKA1 + ANGKA2))
        ;;
    -)
        HASIL=$((ANGKA1 - ANGKA2))
        ;;
    \*)
        HASIL=$((ANGKA1 * ANGKA2))
        ;;
    /)
        if [ $ANGKA2 -eq 0 ]; then
            echo "Error: Tidak bisa membagi dengan nol!"
            exit 1
        fi
        HASIL=$((ANGKA1 / ANGKA2))
        ;;
    *)
        echo "Error: Operator tidak dikenal."
        exit 1
        ;;
esac

echo "Hasil: $ANGKA1 $OPERATOR $ANGKA2 = $HASIL"
```


## 3. hasil uji coba
### beri izin eksekusi dulu:
```
chmod +x ~/praktikum-os/week09/scripts/kalkulator.sh
```
### hasilnya:
<img width="1480" height="551" alt="Screenshot 2026-05-01 134958" src="https://github.com/user-attachments/assets/f6e607ea-7873-4cae-88c0-98e75f0aebd9" />

Berdasarkan pengujian yang dilakukan di terminal, script berjalan dengan skenario sebagai berikut:

### Operasi Berhasil:

* Input: ./kalkulator.sh 20 + 5 → Output: Hasil: 20 + 5 = 25
* Input: ./kalkulator.sh 10 \* 5 → Output: Hasil: 10 * 5 = 50
* Input: ./kalkulator.sh 10 / 2 → Output: Hasil: 10 / 2 = 5

### Penanganan Error (Validasi):

* Saat memasukkan ./kalkulator.sh 20+8 (tanpa spasi antar argumen), sistem mendeteksi argumen tidak lengkap karena 20+8 dianggap sebagai satu kesatuan ($1), sedangkan $2 dan $3 kosong.
* Saat hanya memasukkan satu angka ./kalkulator.sh 5, sistem menampilkan pesan error dan memberikan instruksi penggunaan yang benar.

