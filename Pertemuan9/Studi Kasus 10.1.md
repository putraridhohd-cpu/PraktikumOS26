# Studi Kasus 10.1 Server Lambat karena Memori

## Langkah 1: Periksa kondisi memori secara keseluruhan.
<img width="1212" height="128" alt="image" src="https://github.com/user-attachments/assets/d67f5b16-8de4-4c60-81f4-ef825afb9886" />

## Langkah 2: Pantau proses secara real-time.
<img width="1478" height="1055" alt="4535388d-d58d-452c-988b-152670d23a1c" src="https://github.com/user-attachments/assets/9f118957-6028-4d78-b8ce-799c1915f00e" />

## Analisis
### 1. Apakah nilai available sangat kecil (misalnya di bawah 200 MB pada server dengan RAM 2 GB)? Jika ya, server kemungkinan kekurangan memori.
Nilai available pada sistem di gambar masih 1.6Gi, yang berarti masih dibawah 200 MB, jadinya server tidak mengalami kekurangan memori.
<img width="421" height="67" alt="image" src="https://github.com/user-attachments/assets/cbfbf4ce-ee2a-480e-987e-fc8255abff2a" />

### 2. Apakah kolom used pada baris Swap lebih dari 0? Jika ya, kernel sedang menggunakan swap, yang berarti performa menurun.
Kolom used di baris Swap itu masih 0B, berarti kernel belum sama sekali menggunakan swap dan performa sistem masih terjaga karena seluruh data diproses di RAM.
<img width="249" height="63" alt="image" src="https://github.com/user-attachments/assets/a603a857-70db-43f8-8b82-808190104b1f" />

### 3.  Di tampilan top, proses apa yang memiliki %MEM terbesar? Proses tersebut menjadi kandidat utama penyebab lambatnya server.
Di tampilan top, proses dengan %MEM terbesar adalah PID 1 dengan penggunaan 0.7%,tapi itu masih kecil jadi nya gak bakal membuat lambat server.
<img width="656" height="98" alt="image" src="https://github.com/user-attachments/assets/7e226e80-7c77-464b-9ff6-8bcab056141f" />
