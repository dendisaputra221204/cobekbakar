# Cobek Bakar — Aplikasi Kasir 

Deskripsi singkat  
Cobek Bakar adalah aplikasi kasir sederhana untuk restoran atau warung makan. Aplikasi ini memfasilitasi proses transaksi penjualan, manajemen menu, pencetakan struk, dan pembuatan laporan harian/bulanan untuk membantu operasional kasir dan pemilik usaha.

Ringkasan tujuan & masalah yang diselesaikan
- Mempercepat proses transaksi di kasir (input pesanan, hitung total, cetak struk).
- Menyederhanakan manajemen menu dan stok (tambah/ubah/hapus menu).
- Menghasilkan laporan penjualan harian/bulanan untuk rekonsiliasi dan analisis.
- Mengurangi kesalahan perhitungan manual dan pencatatan kertas.

Fitur utama
- Login per pengguna (kasir / admin)
- Manajemen menu (CRUD)
- Proses transaksi penjualan (tambah item, hitung total, diskon, pembayaran)
- Cetak struk penjualan (thermal printer / browser print)
- Cetak laporan penjualan (harian, bulanan, periode)
- Manajemen user (opsional, tergantung implementasi)

Teknologi yang digunakan
- Bahasa server: PHP (native / procedural)  
- Database: MySQL / MariaDB  
- Frontend: HTML, CSS, JavaScript (kemungkinan menggunakan Bootstrap)  
- Web server: Apache / Nginx (biasa dijalankan lewat XAMPP/LAMP/WAMP)  
- (Opsional) Library/Tool untuk cetak PDF atau struk: TCPDF, FPDF, atau cetak lewat window.print / ESC/POS untuk printer thermal

Cara menjalankan aplikasi di localhost (panduan umum)
1. Persiapan lingkungan  
   - Pasang PHP (≥7.0 direkomendasikan), MySQL / MariaDB, dan web server (XAMPP/WAMP/LAMP/MAMP).  
   - Pastikan phpMyAdmin atau tool sejenis tersedia untuk import database.

2. Clone repository
   - git clone https://github.com/dendisaputra221204/cobekbakar.git
   - Salin folder hasil clone ke folder web server Anda, misal:
     - XAMPP: C:\xampp\htdocs\cobekbakar
     - Linux (apache): /var/www/html/cobekbakar

3. Buat database dan import struktur data  
   - Buat database baru, misal: cobekbakar  
   - Import file dump SQL yang ada di repo (jika tersedia). Umumnya file dump berada di folder seperti `database/`, `sql/`, atau bernama `dump.sql` / `cobekbakar.sql`.  
   - Jika tidak menemukan file SQL dalam repo, Anda perlu membuat skema database sesuai file koneksi atau minta file SQL dari pengembang.

4. Konfigurasi koneksi database  
   - Buka file konfigurasi koneksi database (umumnya bernama `config.php`, `koneksi.php`, `db.php`, atau berada di folder `inc/` / `app/`).  
   - Sesuaikan detail koneksi:
     - host: `localhost`
     - username: `root` (atau user DB Anda)
     - password: (kosong atau sesuai)
     - database: `cobekbakar` (nama yang Anda buat)
   - Contoh snippet konfigurasi (ilustrasi):
     ```php
     <?php
     $db_host = 'localhost';
     $db_user = 'root';
     $db_pass = '';
     $db_name = 'cobekbakar';
     $conn = mysqli_connect($db_host, $db_user, $db_pass, $db_name);
     if (!$conn) { die("Koneksi gagal: " . mysqli_connect_error()); }
     ?>
     ```

5. Jalankan server dan akses aplikasi  
   - Start Apache & MySQL (mis. melalui XAMPP Control Panel).  
   - Buka browser dan akses:
     - http://localhost/cobekbakar/login.php
     - atau jika ditempatkan di virtual host, akses sesuai domain lokal Anda.

Akun demo
- Kasir
  - Username: admin
  - Password: admincobekbakar

Link deployment (demo online)
- https://websitecobekbakar.wuaze.com/login.php

Catatan penting & tips untuk fitur cetak struk dan cetak laporan
- Cetak struk (thermal printer):
  - Jika aplikasi menyediakan tombol cetak yang membuka halaman struk, biasanya menggunakan window.print() di JavaScript. Pastikan ukuran kertas di print dialog disesuaikan (mis. 58mm atau 80mm).
  - Untuk integrasi langsung dengan printer thermal (ESC/POS), diperlukan driver atau middleware (contoh: menggunakan server-side library ESC/POS-php atau aplikasi middleware di client).
  - Tes cetak pada browser terlebih dahulu; bila hasil perlu penyesuaian layout, ubah CSS khusus untuk cetak (@media print).
- Cetak laporan (PDF / XLS / CSV):
  - Untuk PDF, gunakan library server-side seperti TCPDF / FPDF untuk menghasilkan file PDF yang dapat diunduh.
  - Untuk eksport ke Excel/CSV, bangun endpoint yang mengeluarkan header CSV/XLS dan isi baris data sesuai laporan.
  - Pastikan filter periode tanggal bekerja dengan benar (dari/tanggal sampai) untuk laporan yang akurat.
- Pengujian:
  - Lakukan pengujian cetak di lingkungan yang sama dengan printer target (mis. komputer kasir terhubung printer).
  - Periksa setting charset dan encoding saat menghasilkan PDF/CSV agar nama menu/karakter khusus tampil benar.

Tips tambahan & pemeliharaan
- Backup database secara rutin (otomatis atau manual) untuk mencegah kehilangan data.
- Batasi akses file konfigurasi (set permissions) agar kredensial DB tidak mudah diakses.
- Pertimbangkan menambahkan validasi input dan sanitasi untuk mencegah SQL injection.
- Jika ingin multi-user/role, kembangkan manajemen user dengan hak akses (role-based).

Lisensi & Kontribusi
- Jika belum ada file LICENSE di repo, tambahkan lisensi yang sesuai (MIT, Apache-2.0, dsb.) untuk memperjelas penggunaan dan kontribusi.
- Untuk kontribusi, tambahkan file CONTRIBUTING.md berisi panduan menambahkan fitur, format commit, dan cara menjalankan test (jika ada).

Kontak / Pemilik proyek
- Pemilik repo: dendisaputra221204 (lihat halaman repo untuk detail kontak)

---

Dokumentasi ini saya susun agar pembaca (developer baru, pemilik usaha, atau pengguna kasir) dapat cepat memahami tujuan dan cara menjalankan aplikasi. Jika Anda mau, saya bisa:
- Menambahkan contoh file `config.php` lengkap untuk dimasukkan ke repo,
- Membuat template SQL (schema) jika Anda belum memiliki dump database,
- Menulis panduan integrasi printer thermal (ESC/POS) atau contoh pembuatan laporan PDF.

Sebagai langkah selanjutnya, saya dapat langsung membuat file README.md ini di repositori jika Anda ingin — beri konfirmasi supaya saya membuat commit/PR.
