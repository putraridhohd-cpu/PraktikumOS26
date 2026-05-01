# Praktikum 7.4: Library Fungsi Validasi

## 1. buat file library
buat file lib.validasi.sh nya di nano (pastikan sudah ada di directory scripts),lalu isi dengan kode program ini:
<img width="1113" height="581" alt="image" src="https://github.com/user-attachments/assets/a43ff57f-46f5-431b-ac76-de73df402d1a" />

simpan lalu keluar

## 2. buat file utama nya (pakai-library.sh)
Script ini yang akan memanggil (source) library di atas
<img width="1215" height="747" alt="image" src="https://github.com/user-attachments/assets/4b1ba13b-cb2d-4a59-b01f-3964cfc5153a" />

## 3. Beri izin dan uji semua skenario:
<img width="1116" height="382" alt="image" src="https://github.com/user-attachments/assets/0ab1100b-d695-4743-ab7b-c0cee53e0a79" />



# Latihan 9.4: Fungsi Konfirmasi

## 1. Update lib-validasi.sh
modifikasi file nano lib-validasi tadi:
<img width="692" height="449" alt="image" src="https://github.com/user-attachments/assets/633550eb-bd7c-4df0-a64f-8dc1b44f95a5" />

## 2. buat Script Baru: hapus-file.sh 
buat script baru bernama hapus-file dan isi lode program ini didalamnya:
<img width="1173" height="696" alt="image" src="https://github.com/user-attachments/assets/96de449b-695c-46b2-a4db-87c3a874a39b" />

## 3. kita buat file yang akan di tes hapus nya
<img width="1652" height="177" alt="image" src="https://github.com/user-attachments/assets/933c0175-c392-4376-ac83-2c07d1f3b9f9" />

## 4. kita beri izin dengan chmod +x lalu eksekusi saja:
<img width="1635" height="241" alt="image" src="https://github.com/user-attachments/assets/b795ae31-243e-4402-bfe8-1d1525daefde" />

bisa terlihat disitu kalau file test.txt nya sudah terhapus di ls nya

## 5. Analisis
Konsep source pada Bash sangat mirip dengan import pada bahasa Java yang biasa saya gunakan di kuliah PBO. Hal ini memudahkan pengelolaan kode karena fungsi validasi yang sering dipakai tidak perlu ditulis ulang di setiap script baru, cukup diletakkan dalam satu file library pusat.
